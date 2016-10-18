
## Results
我是在第105次发生死锁  
![105dead](https://github.com/LLuqw/ES2016_14353219/blob/master/Deadlock_lab/105_dead.jpg?raw=true)  

## 死锁产生的四个条件  
    * 互斥条件：一个资源每次只能被一个进程使用  
    * 请求与保持条件：当线程请求资源被阻塞时，仍然占有已获得的资源，不释放  
    * 不剥夺条件：进程已经获得的资源，再使用完毕之前，不会强行剥夺  
    * 循环等待条件：若干进程之间形成一种头尾相接的循环等待资源关系  
## 分析原因  
先看一波主要代码，至于bat就只是让这个程序跑1000次而已  
![code](https://github.com/LLuqw/ES2016_14353219/blob/master/Deadlock_lab/code.jpg?raw=true)  
主要是有**synchronized**这个关键字：  

- 当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码  
- 当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。  


可以看到主函数在这个Deadlock类中，他会new一个线程t，然后t.start(),这样线程t就被插入到调度队列中，为就绪状态，当调度到他的时候就会执行run().  
所以大概的流程就是new Thread，然后while(count-->0),然后时间片轮转，所以线程t就会被调度，执行methodB(),假如整个执行完了就会打印出`Inside A.last()`，while跑完之后就是methodA，会打印出`Inside B.last()`,主线程完成，结束。  
那么产生死锁的原因是：每次运行java程序时，当while循环跑完时线程t还没执行完毕的话，就会轮到主线程，这时线程t就会还占有一些资源。假如b想要去调用a.last()时被中断了,那a就没办法调用methodA,，因为无法同时访问一个object中的两个synchronized代码块；当然也有可能时b还在执行methodB时被中断了,所以到a时要调用b.last()当然也被阻塞。  
至于这个随机产生死锁，可能是每次分配的时间片不同导致的，假如时间片在while循环跑一半时完了，那么就是线程t被调度，但是这个时间片不足以让线程t全部执行完毕，所以又是主线程被调度，此时while循环跑完，而且a调用methodA()，但是线程t还占有资源，这时就会出现上面分析的那种死锁情况。




