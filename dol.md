
- Example1结果
![example1](https://github.com/LLuqw/ES2016_14353219/blob/master/image/ex1.jpg?raw=true)
- Example2结果
![example2](https://github.com/LLuqw/ES2016_14353219/blob/master/image/ex2.jpg?raw=true)
- 修改方法
    - example1
    在square.c代码中，我们对i是进行了i=i*i，这样得到的结果就是平方，所以要改成三次方，也只需要改成i=i*i*i
    - example2
    这次是要将square从三次改为两次，因为这里是在xml文件中写的，所以我们需要修改example2.xml这个文件，我们可以发现有一个iterator模块的迭代次数为N,迭代的文件为square.c，然后N的value是3，所以我们只需要将N的值由3改成2即可
    - **tips:每次修改完代码之后都要将build/bin/main文件下对应的那个example文件夹删了，然后在dol的根目录下重新编译 `ant -f build_zip.xml all` ,然后运行`ant -f runexample.xml -Dnumber=X`才能生效,X是要运行哪个例子**
- 感想
 记录下xml中出现的标签
 * process 进程，就是上面图中那些generator，square，consumer的图形，里面主要有说明这个进程的端口，这个进程的源码
 * sw_channel 通道，也就是上图中的那些线，同样需要定义两个端口，分别为input，output
 * connection 连接，就是将进程跟通道连起来，有origin(指定起始端点)，target(指定目标端点)，因此**一个通道会有两个connection**
 * variable 变量 定义了变量名跟数值
 * iterator 迭代，其实就是类似循环的东西
