# threadPool
一个基于C++ 14 17 开发【可变参模板实现的线程池】

Function directory:
- map和queue容器【线程管理和任务调度】
- condition_variable和互斥锁mutex实现任务提交线程｜任务执行线程间的通信机制
- fixed固定线程池数量和cached动态线程数量的线程池定制
- 可变参模板编程+引用折叠，实现线程池submitTask接口，支持任意任务函数和任意参数
的传递 
- 用future和packaged_task模式定制submitTask异步提交任务的返回值

项目问题：
- 线程的资源回收，等待线程池里面所有线程退出时，却发生死锁问题，导致主进程无法退出！！！
- 在windows平台下运行良好的线程池，在linux平台下运行发生死锁问题，平台运行结果不一致！！！

解决方案：
linux下通过gdb attach到正在运行的进程，通过info threads，thread tid，bt等命令查看各个子线程的调用
堆栈信息，一行一行定位项目代码，最终定位到发生死锁的代码位置，分析死锁问题发生的原因，最终解决
