# 协程

协程又称微线程, 是一种用户态的轻量级线程,即协程是由用户程序自己控制调度的.
- 子程序切换由程序自身控制, 因此没有线程切换的开销
- 不需要多线程中共享变量的锁机制, 因为协程在同一个线程中不存在变量冲突

子程序(或者称为函数)的调用是通过栈实现的, 一个线程就是执行一个子程序. 调用总是一个入口, 一次返回, 调用顺序是明确的.

协程看上去也是子程序, 但执行过程中, 可以在子程序内部中断, 转而执行其他的子程序, 在适当的时候再返回来接着执行.


## Python使用generator和yield实现协程

```python
import time

# consumer函数是一个generator(生成器)
def consumer():
    r = ''
    while True:
        # consumer通过yield拿到消息,处理,又通过yield把结果传回
        n = yield r
        if not n:
            return
        print('[CONSUMER] Consuming %s...' % n)
        time.sleep(1)
        r = '200 OK'

def produce(c):
    # 调用c.next()启动生成器
    c.next()
    n = 0
    while n < 5:
        n = n + 1
        print('[PRODUCER] Producing %s...' % n)
        # c.send(n)切换到consumer执行
        r = c.send(n)
        print('[PRODUCER] Consumer return: %s' % r)
    # produce决定不生产了,通过c.close()关闭consumer,整个过程结束
    c.close()

if __name__=='__main__':
    c = consumer()
    produce(c)

```


gevent是一个第三方库, 基于greenlet实现协程

## [asyncio异步模块](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001432090954004980bd351f2cd4cc18c9e6c06d855c498000)

## 相关文章

- [协程](https://blog.csdn.net/ayhan_huang/article/details/75566740)