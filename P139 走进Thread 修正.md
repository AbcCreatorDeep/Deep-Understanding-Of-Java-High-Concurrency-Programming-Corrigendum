# P139 走进Thread 修正

接下来我们来看看线程的运行状态有哪些。

1. NEW：未启动状态

2. RUNNABLE：运行状态

3. BLOCKED：线程正在等待监视器锁；正在synchronized块/方法上等待获取锁，或调用了Object.wait()，等待重新获取锁（修正为：线程正在等待监视器锁，也即正在synchronized块/方法上等待获取锁。）

4. WAITING：等待线程的状态;

   a) 调用Object.wait()、Thread.join()、LockSupport.park()会进入该状态，这里都没设置超时。

   b) 处于等待状态的线程正在等待另一个线程执行特定操作。

   c) 调用Object.wait()的线程等待另一个线程调用Object.notify()、Object.notifyAll()

   d) 调用了Thread.join()的线程等待指定线程终止。

5. TIMED_WAITING：具有指定等待时间的等待线程的线程状态

   调用Thread.sleep(超时时间)、Object.wait(超时时间)、LockSupport.parkNanos、LockSupport.parkUntil会进入该状态，这里均设置了超时

6. TERMINATED：线程已经终止，已经执行完成的线程状态