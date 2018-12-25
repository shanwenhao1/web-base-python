# 进程

进程: 一个具有一定独立功能的程序关于某个数据集合的一次运行活动, 是系统进行资源分配和调度运行的基本单位.
- 用某种方法将相关的资源集中在一起. 进程有存放程序正文和数据以及其他资源的地址空间。
- 进程拥有一个执行的线程，可以简写为线程。

## 进程与程序的差别

进程是一个动态的概念
- 进程是程序的一次执行过程, 是动态概念
- 程序是一组有序的指令集合, 是静态概念

当操作系统要完成某个任务时, 它会创建一个进程, 当进程完成任务之后, 系统就会撤销这个进程, 收回它所占用的资源.

从结构上讲, 每个进程都由程序、数据和一个进程控制块(Process Control Block, PCB)组成.

进程可以创建子进程


## Python multiprocessing模块

python中使用multiprocessing模块创建子进程

```python
from multiprocessing import Process
import os

# 子进程要执行的代码
def run_proc(name):
    print('Run child process %s (%s)...' % (name, os.getpid()))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    # Process创建子进程, 需传入执行函数和函数的参数
    p = Process(target=run_proc, args=('test',))
    print('Child process will start.')
    p.start()
    p.join()
    print('Child process end.')
```

使用进程池的方式批量创建子进程, python Pool的默认大小是CPU的核数, 超过CPU核数时的子进程会等待
```python
from multiprocessing import Pool
import os, time, random

def long_time_task(name):
    print('Run task %s (%s)...' % (name, os.getpid()))
    start = time.time()
    time.sleep(random.random() * 3)
    end = time.time()
    print('Task %s runs %0.2f seconds.' % (name, (end - start)))

if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Pool(4)
    for i in range(5):
        p.apply_async(long_time_task, args=(i,))
    print('Waiting for all subprocesses done...')
    # 调用join()之前需调用close(), 之后就不能再添加新的Process了
    p.close()
    # join()方法会等待所有子进程执行完毕
    p.join()
    print('All subprocesses done.')
```

multiprocess中使用Queue、Pipes等多种方式来交换数据.



## 相关文章

- [进程的概念](https://www.cnblogs.com/tianlangshu/p/5224178.html)
- [进程详解](https://www.cnblogs.com/jacklu/p/5317406.html)