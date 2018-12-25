# 线程

传统操作系统中, 每个进程有一个地址空间和一个控制线程

## 线程的使用

- 在许多应用中同时发生多种活动.其中某些活动随着时间的推移会被阻塞,
通过将这些应用程序分解成可以准并行运行的多个顺序线程,程序设计模型会变得更简单
- 在许多应用中同时发生多种活动.其中某些活动随着时间的推移会被阻塞,通过将这些应用程序分解成
可以准并行运行的多个顺序线程,程序设计模型会变得更简单
- 使用线程可以加强程序的性能
- 在多CPU系统中,多线程是有益的

### 线程与进程的区别

- 同一个进程的线程之间共享该进程的公共内存.所以它们可以访问同一个文件(线程可以访问进程
地址空间中的每一个内存地址)
- 不同进程之间共享整个内存空间,但是每个进程只能访问特定的地址空间
- 进程将资源集中在一起, 而线程则是在CPU上被调度执行的实体.

## 线程模型

进程模型基于两种独立的概念：资源分组处理与执行.将这两种概念分离开会更有益,这就引入了线程这一概念.

线程的状态:
- 运行
- 阻塞
- 就绪
- 终止

每个线程都有自己的一帧堆栈,供各个被调用但是还没有从中返回的过程使用.在该帧中存放了相应过程的局部变量以及
过程调用完成之后使用的返回地址.通常每个线程会调用不同的过程,从而有不同的执行历史.
这就是为什么每个线程需要有自己堆栈的原因.

## Python _thread和threading模块

threading模块是高级模块, 在_thread基础上进行封装

```python
import time, threading

# 新线程执行的代码:
'''由于任何进程默认就会启动一个线程,我们把该线程称为主线程,主线程又可
以启动新的线程,Python的threading模块有个current_thread()函数,它永远
返回当前线程的实例.主线程实例的名字叫MainThread,子线程的名字在创建时指定,
我们用LoopThread命名子线程.名字仅仅在打印时用来显示,完全没有其他意义,
如果不起名字Python就自动给线程命名为Thread-1,Thread-2……
'''
def loop():
    print('thread %s is running...' % threading.current_thread().name)
    n = 0
    while n < 5:
        n = n + 1
        print('thread %s >>> %s' % (threading.current_thread().name, n))
        time.sleep(1)
    print('thread %s ended.' % threading.current_thread().name)

print('thread %s is running...' % threading.current_thread().name)
t = threading.Thread(target=loop, name='LoopThread')
t.start()
t.join()
print('thread %s ended.' % threading.current_thread().name)
```

由于同一个进程中的多线程共享变量, 因此有的时候就需要锁

```python
import time, threading

# 假定这是你的银行存款:
balance = 0
lock = threading.Lock()

def change_it(n):
    # 先存后取，结果应该为0:
    global balance
    balance = balance + n
    balance = balance - n

def run_thread(n):
    for i in range(100000):
        # 先要获取锁, 只有一个线程能成功获取锁:
        lock.acquire()
        try:
            # 放心地改吧:
            change_it(n)
        finally:
            # 改完了一定要释放锁:
            lock.release()

t1 = threading.Thread(target=run_thread, args=(5,))
t2 = threading.Thread(target=run_thread, args=(8,))
t1.start()
t2.start()
t1.join()
t2.join()
print(balance)
```

虽然Python的线程是真正的线程, 但是由于解释器执行代码时GIL锁的存在导致不能利用多线程实现多核任务.
因此可用多进程 + 协程实现高并发. 


## 相关文章

- [线程](https://blog.csdn.net/qq_33102061/article/details/54290079)
- [多线程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/00143192823818768cd506abbc94eb5916192364506fa5d000)
- [GIL锁详解](http://cenalulu.github.io/python/gil-in-python/)