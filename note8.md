# 多线程 vs 多进程
- 程序：一堆代码以文本形式存入一个文档
- 进程：程序运行的一个状态
    - 包含地址空间、内存、数据栈等
    - 每个进程有自己完全独立的运行环境，多进程共享数据是一个问题
- 线程
    - 一个进程的独立运行片段，一个进程可以有多个线程
    - 轻量化的进程
    - 一个进程的多个线程间共享数据和上下文环境
    - 共享互斥问题
- 全局解释器锁（GIL）
    - Python代码的执行时由python的虚拟机进行控制
    - 在主循环中只能有一个控制线程在执行
- Python包
    - thread：有问题，不好用，python3中改成了_thread
    - threading：通行的包
- threading的使用
    - 直接使用threading.Thread生成Thread实例
        - 1.t = threading.thread(target=xxx, args=(xxx,))
        - 2.t.start()：启动多线程
        - 3.t.join()：等待多线程执行完成
- 守护线程 - daemon
    - 如果在程序中将子线程设置成守护线程，则子线程会在主线程结束的时候自动退出
    - 一般认为，守护线程不重要或者不允许离开主线程独立运行
    - 守护线程案例能否有效果跟环境相关
    
-线程常用属性
    - threading.currentThread：返回当前线程变量
    - threading.enumerate:返回一个包含正在运行的线程的list，正在运行的线程指的是线程启动后，结束前的状态
    - threading.activeCount：返回正在运行的线程数量
    - thr.setName：给线程设置名字
    - thr.getName：得到线程的名字
    
    
- 还可以直接继承自threading.Thread
    - 直接继承Thread
    - 重写run函数
    - 类实例直接使用
    
    
- 共享变量 
    - 共享变量：当多个线程同时访问一个变量的时候，会产生共享变量的问题
    - 解决变量：锁、信号灯
    - 锁：
        - 是一个标志，表示一个线程在占用一些资源
        - 使用方法：
            - 上锁
            - 使用共享资源
            - 取消锁，释放锁
        - 锁谁：哪个资源需要多个线程共享，锁哪个
        - 理解锁：锁其实不是锁住谁，而是一个令牌
    - 线程安全问题：
        - 如果一个变量/资源，他对于多线程来讲，不用加锁也不会引起任何问题，则称为线程安全
        - 线程不安全变类型：list，set，dict
        - 线程安全变量类型：queue
        
    - 生产者消费者问题
        - 一个模型，可以用来搭建消息队列
        - queue是一个用来存放变量的数据结构，特点是先进先出，内部元素需要进行排队
       
    - 死锁问题
    - 锁的等待时间问题
    - semaphore
        - 允许一个资源最多有几个多线程同时使用
    - threading.Timer
        - Timer是利用多线程，在指定时间后启动一个功能
        
    - 可重入锁
        - 一个锁，可以被一个线程多次申请
        - 主要解决地柜调用的时候，需要申请锁的情况
        
        
# 线程替代方案
- subprocess
    - 完全跳过线程，使用进程
    - python2.4后引入
- mutiprocessing
    - 使用threading的接口派生，使用子进程
    - 允许为多核或者多cpu派生进程，接口跟threading非常相似
    - python2.6引入
- concurrent.futures
    - 新的异步执行模块
    - 任务级别的操作
    - python3.2后引入
  
# 多进程
- 进程间通讯(InterprocessCommunication,IPC)
- 进程之间无任何共享状态
- 进程的创建
    - 直接生成Process实例对象
    - 派生子类
- 在os中查看pid、ppid以及他们的关系
- 生产者消费者模型
    - JoinableQueue
    - 队列中哨兵的使用
    
# 协程
- 资料在收藏夹

# 迭代器
- 可迭代（Iterable）：直接作用于for循环的变量
- 可迭代（Iterator）：不但可以作用于for循环，还可以被next调用
- list是典型的可迭代对象，但不是迭代器
- 可以通过isinstance判断是否可迭代或是否是迭代器
- iter函数可以试想可迭代与迭代器之间的转化

# 生成器
- generator：一边循环一边计算下一个元素的机制/算法
- 需要满足三个条件：
    - 每次调用都生产出for循环需要的下一个元素
    - 如果到达最后一个后，报出StopIteration异常
    - 可以被next函数调用
- 如何生成一个生成器
    - 直接使用（用[]是列表生成器，用()则就是生成器）
    - 如果函数中包含yield，则这个函数就叫生成器
    - next调用函数，遇到yield返回
    
#协程
- 历史进程
    - 3.4引入协程，用yield实现
    - 3.5引入协程语法
    - 实现的协议比较好的包邮asyncio、tornado、gevent
- 定义：协程是为非抢占式多任务产生子程序的计算机程序组件，协程允许不同入口点在不同位置暂停或者开始执行程序。
- 从技术角度讲，协程就是一个你可以暂停执行的函数，或者干脆把协程理解为生成器
- 协程的实现：
    - yield返回
    - send调用
- 协程的四个状态
    - inspect.getgeneratorstate(...)函数确定，该函数会返回下述字符串中的一个：
    - GEN_CREATED：等待开始执行
    - GEN_RUNNING：解释器正在执行
    - GEN_SUPEND：在yield表达式处暂停
    - GEN_CLOSED：执行结束
    - next预激
- 协程终止
    - 协程中未处理的异常会向上冒泡，传给next函数或send函数的调用方（即触发协程的对象）
    - 终止协程的一种方式：发送某个哨符值，让协程退出。内置的None和Ellipsis等常量经常用作哨符值
- yield from
    - 调用协程为了得到返回值，协程必须正常终止
    - 生成器正常终止会发出StopIteration异常，异常对象的value属性保存返回值
    - yield from从内部捕获StopIteration异常
    - 委派生成器
        - 包含yield from表达式的生成器函数
        - 委派生成器在yield from表达式处暂停，调用方可以直接把数据发给子生成器
        - 子生成器在把产出的值发给调用方
        - 子生成器在最后，解释器会抛出StopIteration，并且把返回值附加到异常对象上
        
        
# asyncio
- python3.4开始引入标准库当中，内置对异步io的支持
- asyncio本身是一个消息循环
- 步骤
    - 创建消息循环
    - 把协程导入
    - 关闭
    
# async and await
- 为了更好的表示异步io
- python3.5引入
- 让协程代码更简洁
- 使用上，可以简单的进行替换
    - 用async替换@asyncio.coroutine
    - await替换yield from
    

# aiohttp
- asyncio实现单线程的并发io，在客户端用处不大
- 在服务器端可以asyncio+coroutine配合，因为http是io操作
- asyncio实现了tcp，udp，ssl等协议
- aiohttp是给予asyncio实现的http框架
- pip install aiohttp安装


# concurrent.futures
- python3新增的库
- 类似其他语言的线程池的概念
- 利用multiprocessing实现真正的并行计算（cpu得有多个核）
- 核心原理：以子进程的形式，并行运行多个python的解释器，从而令python程序可以利用多核
cpu来提升执行速度。由于子进程与主解释器相分离，所以他们的全局解释器锁也是相互独立的。
每个子进程都能够完整的使用一个cpu内核
- concurrent.futures.Executor
    - ThreadPoolExecutor
    - ProcessPoolExecutor
    - 执行的时候需要自行选择使用上述哪个
- submit(fn, args, kwargs)
    - fn：异步执行函数
    - args，kwargs：参数



# current中的map函数
- map(fn, *iterables, timeout=None)
    - 跟map函数类似
    - 函数需要异步执行
    - timeout：超时时间
    - map跟submit使用一个就行
# Future


