# ES2016_14353219

### Description    
   - [http://www.tik.ee.ethz.ch/~shapes/dol.html](http://www.tik.ee.ethz.ch/~shapes/dol.html) dol介绍..  
   
------------

### How to install（下面安装配置DOL教程以ubuntu为例）
 1. 配置必要的实验环境：
    * `$	sudo apt-get update`
    * `$	sudo apt-get install ant`
    * `$ 	sudo apt-get install openjdk-7-jdk`
    * `$	sudo apt-get install unzip`  
    上面四个命令是安装我们配置DOL过程中需要用到的ant,openjdk,unzip等工具,其中[ant工具介绍](http://blog.163.com/qiangyongbin2000@126/blog/static/77517819201151653423687)，unzip是一个解压工具，jdk就可以不用介绍了=。=
 2. 下载dol跟systemc两个，下载地址如下，下载完可以直接拉到vmware的虚拟机中去,放在home下的根目录即可  
    [http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz)  
    [http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip](http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip)
 3. 解压文件  
    `$	mkdir dol`新建dol文件夹  
    `$	unzip dol_ethz.zip -d dol` 将dol_ethz.zip解压到dol文件夹中  
    `$	tar -zxvf systemc-2.3.1.tgz` 解压systemc  
 4. 编译systemc  
    `$	cd systemc-2.3.1`在上一步我们解压后就进入systemc的目录下  
    `$	mkdir objdir` 新建一个临时文件夹objdir  
    `$	cd objdir` 进入该文件夹  
    `$	../configure CXX=g++ --disable-async-updates`   运行configure(能根据系统的环境设置一下参数，用于编译)  
下面是运行configure后的结果：  
    ![configure结果](https://github.com/LLuqw/ES2016_14353219/blob/image/configure%E7%BB%93%E6%9E%9C.jpg?raw=true)
    `$	sudo make install `编译systemc  
编译后执行`$ cd .. ` 返回上级目录` $ ls`：打印出所在目录下的所有文件夹跟文件，可以看到如下结果：  
![ls查看](https://github.com/LLuqw/ES2016_14353219/blob/image/ls%E6%9F%A5%E7%9C%8B.jpg?raw=true)  
    `$	pwd` 输出当前路径，接着有用  
![pwd](https://github.com/LLuqw/ES2016_14353219/blob/image/pwd.jpg?raw=true)  
 5. 编译dol  
    `$	cd ../dol` 进入刚刚新建dol文件夹  
    `sudo gedit build_zip.xml`                   用这个命令可以获得最高权限，这样就能对build_zip.xml进行修改，也可以直接找到这个文件，然后右键open with,然后选择gedit，如果这样进入后x无法修改就还是用终端用sudo打开就能修改，进去后找到
> property name="systemc.inc" value="YYY/include"  
> property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"

    把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）
插入结果如下:  
    ![build_zip](https://github.com/LLuqw/ES2016_14353219/blob/image/build_zip.jpg?raw=true)  
    `$	ant -f build_zip.xml all` 接着编译这个东西，成功的话就会显示build successful  
 6. 运行与测试  
    `$	cd build/bin/main` 进入build/bin/main路径下  
    `$	ant -f runexample.xml -Dnumber=1`运行第一个例子  
    运行完出现下面就说明配置成功了  
    ![example](https://github.com/LLuqw/ES2016_14353219/blob/image/example.jpg?raw=true)  

----------
### Experimental experience

 - 配置dol环境过程中，遇到的唯一问题就是build_zip.xml修改没成功，所以最后build fail，然后重新修改完之后就build successful了，用的系统是ubuntu14.04，32位
 ![ubuntu](https://github.com/LLuqw/ES2016_14353219/blob/image/ubuntu.jpg?raw=true)  
