# learning

## Git
### git相关概念
   - git HEAD
        HEAD可以指向一个branch(大部分情况),也可以指向一个commit,指向一个commit时称其为游离状态 <br />
        每个branch也有一个指向，指向的是本分支的最新commit(也可以通过git branch -f branchName commitID 修改，但是暂时不知道有什么用)<br />
        HEAD---->Branch----->commit ID<br />
        使用 ^ 向上移动 1 个提交记录,使用 ~<num> 向上移动多个提交记录，如 ~3<br />
### git game
   https://learngitbranching.js.org/?NODEMO=&locale=zh_CN <br />
#### git rebase
   rebae与merge命令类似，不过会使commit更加线性，可以理解为把A分支从B分支最后一个改动开始改动 <br />
   https://www.cnblogs.com/zhangsanfeng/p/9575184.html <br />
#### git checkout 
   checkout本质是HEAD的移动<br />
   https://blog.csdn.net/csflvcxx/article/details/81612336<br />
   https://blog.csdn.net/wu_xianqiang/article/details/110678343<br />
#### git reset 与 git revert  
   git reset是用于本地的branch(未push的), **将暂存区的commit回到某个commit的时候**，工作区不动<br />
    git reset --soft HEAD^,将上一个commit吃掉，回到提交前的状态
   git revert是针对远端，通过提交一个新的commit,**撤销某几个commit**（新的commit的改动就是之前的反操作） <br />  
#### git blame
   git想要查看关于某一行的几次commit前的改动(正常只能看一次commit),那么可以回到那次commit的文件，再去查看这行当时是谁改的  
#### git 删除文件
   对于大文件或者私密文件，直接提一个新的commit删除，并不能永久删除，在git clone时依然会下载该文件.所以需要通过filter-branch来删除


    
## Linux
   
   ### NFS与rpcbind
   https://www.cnblogs.com/me80/p/7464125.html<br /> 
   
   ### env与 bashrc,profile
   env的东西保存在bashrc和profile里面。<br /> 
   bashrc和profile在/etc和/home中都存在一份，/home中的相同内容会覆盖/etc中的。bashrc和profile本身也稍有区别<br /> 
   https://cloud.tencent.com/developer/article/1174426<br /> 
   
   ### 正则
   (.+)与(.+?)： (.+)默认是贪婪匹配 (.+?)为惰性匹配   https://www.cnblogs.com/ysk123/p/9896850.html<br /> 
   []中括号中的字符都被视为原始字符，既不带特殊含义
   
   ### scp
   注意，使用scp时，如果最前面加了sudo，则当前登陆用户是root，可能没有对方机器的登陆权限<br /> 
   scp无法直接在target端执行sudo命令，所以只能把文件传输到target用户拥有write权限的目录下<br /> 
   
   ### bash语法
      #### sed
      用于对于多行文本的操作
      #### trap
      对捕获到的SIGNAL,改变原有的处理action为新的action,可以用来做类似try catch的处理(如果单纯重试请使用 xx || xx)
      https://cloud.tencent.com/developer/article/1640249
      解决trap不能继续执行:可以把某个方法作为子脚本执行，这样trap的范围是整个子脚本(要注意在子shell，exit只会退出相关进程，并不会被trap捕捉，所以要对subshell的地方单独处理)
      #### exit与return
      exit是退出程序，return是退出函数（注意，return退出函数时，要保证上层函数同样retrun下层函数的值才行，不然不会传递. 如果有很多层，可以在最底层调用时export 一个变量，在外面去判断变量的值）
      #### ln
      如果涉及到一台机器某个文件需要一个副本的话，可以尝试用软连接(用cp可能导致文件权限改变)

   ### resolv.conf
   /etc/resolv.conf 用于设置DNS服务器的IP地址及DNS域名   

   ### 2 >&1
   https://blog.csdn.net/zhaominpro/article/details/82630528
   2>&1 本身是一个整体，将标准错误重定向到标准输出

## 计算机常识
   ### idrac
   iDRAC又称为Integrated Dell Remote Access Controller，也就是集成戴尔远程控制卡,这是戴尔服务器的独有功能，iDRAC卡相当于是附加在服务器上的一计算机，可以实现一对一的服务器远程管理与监控，通过与服务器主板上的管理芯片BMC进行通信，监控与管理服务器的硬件状态信息.


## JAVA

   ### javaHome
   javahome配置在path中的顺序可能会影响配置效果<br />
   只要javahome的路径在path中就可以
   ### javac
   使用javac xx.java将一个java程序编译为xx.class文件，然后使用java xx执行 ！！(不要加.class)
   ### ClassPath
   在安装java时需要配置classpath,用于搜索.class文件位置。但是1.5以后已经不需要配了<br /> 
   ### 默认路径
   默认的路径是System.getProperty("user.dir"). 但是这个路径可能是变化的，所以最好还是用绝对路径
   ### public class与class
   在定义class时可以用public或者默认权限修饰. public class必须与文件名相同，所以一个.java中只有一个public class,但是可以有无数个class
   ### 编译与解释
   解释执行：将编译好的字节码一行一行地翻译为**机器码** 执行。 <br /> 
   编译执行：以方法为单位，将字节码一次性翻译为**机器码** 后执行。<br /> 
   编译器看到的都是字节码文件！！！！！ <br /> 
   https://www.cnblogs.com/lingz/archive/2018/07/31/9394238.html<br /> 
   ### java项目不能热重启
   由于class文件只有第一次会加载到内存，所以在不重启jvm的情况下，class的改动是无法识别的
   想要实现热重启，需要给每个类创建一个classloader. (因为同一个类在同一个classloader只能load一次，所以每次更换时，对应的classloader也要更换)
   ### 数组
   arraylist每次扩容，扩一半长度<br /> 
   ### protobuf
   是用来进行跨语言的反序列化工具  xx.java ---> 二进制 ----> xx.c
   首先编写.proto文件，然后使用protoc将.proto文件生成为java文件（生成后的java文件自带转换等方法）
   也可以使用maven插件在编译时自动将指定目录的.prto文件转换为.java
   ### Mutable类
   对于需要在函数间修改值的基本数据类型，可以使用Mutablexxx类<br /> 
   ### hashcode与equals
   equals返回boolean,判断两个对象的是否相等<br /> 
   hashcode返回int,用于表示在hash表中的位置<br /> 
   ### hashmap
   hashmap中的Node节点有Hashcode值，因此在扩容时不会重新获取key的hash值，即使key的hash值改变<br /> 
   ### 并发编程   
   #### 线程池
   如何实现线程池：  依靠blockingqueue来实现，核心线程一直while循环来消费队列中的任务  https://www.cnblogs.com/wxwall/p/7050698.html<br /> 
   什么时候使用： 需要去新建线程完成一些small task时（如果持续时间很长的job就没必要使用线程池了）
   ##### ScheduledExecutorService 
   用来实现定时任务的java类
   ##### atomic类
   atomic类本身并不能保证线程安全性，只是保证了可见性。
   多线程下保证atomic在某个范围内
   ```
   while(true) {
            int current = atomicInteger.get();
            int next = (current + 1) % 5;
            if (atomicInteger.compareAndSet(current, next)) {
               return xxx
            }
        }
   ```
   #### cas
   ```
   while(true) {
            int current = xxx.get();
            //业务逻辑
            if (compareAndSet(current, xxx.get())) {
                retrun xxx  //结束
            }
        }
   ```
   #### countdownlunch与cyclebarrier，Semaphore
   countdownlunch: 等待其他几个任务执行完毕之后才能执行,并且是不可重用的
   cyclebarrier: 栅栏，实现让一组线程等待至某个状态之后再全部同时执行，是可重用的
   Semaphore：车位，控制同时访问的线程个数，通过 acquire() 获取一个许可，如果没有就等待，而 release() 释放一个许可
   ### try-catch-with-resource
   java7中的一种新语法，用于try-catch需要关闭资源时使用，很方便。只要资源实现了autoclose接口就可以使用<br /> 
   资源不释放可能导致连接无法断开，尽管有些连接操作会把关闭写在finalize里，但是会有不确定性<br /> 
   https://www.cnblogs.com/barrywxx/p/9993005.html  <br /> 
   https://blog.csdn.net/hengyunabc/article/details/18459463<br /> 
   
   ### ThreadLocal
   https://www.jianshu.com/p/640f2c0ac4b0<br />  
   为什么value不作为弱引用   https://www.zhihu.com/question/399087116<br />  

   ### nio
   #### 零拷贝
   https://blog.csdn.net/weixin_39879073/article/details/123054799   零拷贝的核心是减少了从内核缓冲区copy到jvm内存这个过程
   
   ### stream流
   stream流使用时分为三步： 创建stream-----> 对steam操作 -----> 结束<br /> 
   其中每一步都有很多api   https://blog.csdn.net/y_k_y/article/details/84633001<br /> 
   关于flatmap:  使用情况是当map方法返回的是个集合时(如果返回的是一个集合，用Map得到的结果是类似于这样：list<Person[]> ， 而flatmap则是list<Person>)
   结束时可以对集合进行Collectors.groupby，返回一个map<br /> 
   还可以对两个stream流进行Stream.concat操作<br /> 
   stream流的操作是不改变原始数组的(foreach可以改变，但是要注意foreach时的stream流是否含有元素，如果之前进行了filter导致没有元素则不会改变任何东西)
   foreach与collect无法同时使用，filter作用于不同的结束符效果也不一样
   stream的并行：https://www.jb51.net/article/149901.htm<br /> 

   ### jre/lib/cacerts
   用来储存可以信任的网站的公钥(类似于浏览器信任证书的功能)

   ### IO操作
   - inputWriter<br />
   创建inputWriter对象时，需要传一个boolean参数，用来控制是否为追加输入(默认false)<br />
   
   ### 序列化
   writeObject readObject来实现手动的存储与读取<br /> 
   transient声明的对象不主动序列化<br />
   序列化会自动继承<br />
   ### JVM
#### JIT编译器
###### 为什么不使用aot(静态编译)
JIT编译是动态编译，指字节码---->机器码 这一过程<br /> 
为什么不一上来全弄成机器码,既为什么不采用AOT（静态编译）：  1. 缺少运行环境生成出的机器码，可能效率并不高  2. 空间问题<br /> 
###### 逃逸分析
通过分析变量的作用域，进行以下优化： 同步省略，标量替换，栈上分配<br /> 
https://blog.csdn.net/hollis_chuang/article/details/80922794<br /> 
但是逃逸分析并不成熟，而且分析也需要消耗时间，不一定比直接解释执行来的快<br /> 
#### JVM内存模型
##### 栈
- TLAB (Thread Local Allocation Buffer)
    JVM使用TLAB来避免多线程冲突(比如多个线程同时在堆上创建对象，是需要同步的)，在给对象分配内存时，每个线程使用自己的TLAB，这样可以避免线程同步，提高了对象分配的效率.<br /> 
    https://blog.csdn.net/xiaomingdetianxia/article/details/77688945<br /> 
#### 强软弱虚
   软，弱引用都是在对象没有强引用的情况下发生的
#### 内存分配
   1. 空闲链表（free list）：通过额外的存储记录空闲的地址，将随机 IO 变为顺序 IO，但带来了额外的空间消耗。(标记清除时)<br /> 
   2. 碰撞指针（bump  pointer）：通过一个指针作为分界点，需要分配内存时，仅需把指针往空闲的一端移动与对象大小相等的距离，分配效率较高，但使用场景有限。（标记整理时）<br /> 
#### JVM内存泄漏
几个常见的场景：
1. 静态集合： 静态属性的生命周期一般都是与jvm一样的，所以在设置静态属性时要三思，单例对象也属于这种情况<br /> 
2. 属性作用域不合理： 比如局部变量定义为了全局变量<br /> 
3. map中的key： 当map的key为对象时（string除外），可能会发生key泄露的事。可以使用weakedHashmap<br /> 
4. hashcode变化导致内存泄露： 如果hashcode是可变的，那么会出现无法remove掉set中存在的hashcode,所以一直有引用指向这个对象。 因此hashcode可以改变的对象，在使用哈希表时，要在Hash值改变之前先从Hash表移除<br /> 
当我们创建的引用不想去影响对象的生命周期时，就去使用弱/软引用<br /> 
在list,set等集合中，对于不使用的内部元素，要及时置Null,或者使用weakedxxx(Collections.newSetFromMap();如果后续要进行遍历，则不能用weadxx)<br /> 
#### 垃圾回收
##### cms
- 为什么不采用标记整理
为了追求单次gc时间，cms的清除过程是不stw，如果要整理的话，会造成空指针的问题，所以采用标记清除<br /> 
    
#### JVM调优
##### 调优指标
1. stw时间   
2. 吞吐量（运行时间与总时间的比值）
3. 并发数
##### JVM监控命令(命令行版)
- JPS (java process status)
 显示java进程的进程号，类似于linux的ps命令,可以在启动时 -XX:-UsePerfData 使jps无法检测到该进程
 -q :只显示id   -l: 显示进程完整名称  -v: 显示jvm启动参数 
- JSTAT (JVM statictics monitor tool) 
  用于监控jvm状态的命令，没有gui时使用 
  interval: 查询间隔(默认只查询一次)  count: 设置查询总次数  -t: 显示程序运行总时间
  类加载参数： -class: 显示类装载信息
  编译器相关参数:   
  垃圾回收相关参数：-gc 显示各区域总大小和当前容量，gc次数，时间等  （根据运行时间与gc时间比值，20%以上说明有些压力，90%则随时可能oom;  如果ou列一直不断上生，怀疑是不是内存泄漏）
- JINFO (configuration info for java) 
  用于查看或修改jvm参数 (openjdk8似乎有bug,无法使用jinfo)
  查看参数： -sysprops: 查看system.props的值   -flags: 查看非默认值的参数  -flag: 查看某个参数的值
  修改参数： -flag: 能修改的参数很有限
- JMAP(JVM memory map)
  用于生成dump文件(快照，记录了堆信息等)
  手动： jmap -dump:live,format=b,file=$(path) PID  只保存存活的对象 (手动生成的dump并不是实时的，需要等线程达到安全点才能停止)
  自动： 通过配置jvm参数，在即将oom之前自动触发，自动生成快照  -xx:+HEAPDUMP...  -xx:HEAPDUMPPATH=... 
- JSTACK
  用于显示线程信息,显示各个线程的状态，可以发现死锁等问题
  -l 额外显示锁信息  
##### JVM监控命令(GUI)
- jmx
- jstatd  
- visual vm
  需要下载，手动配置java_home
  还可以 生成/读取 dump文件
  远程监控：   https://www.cnblogs.com/jhxxb/p/13279201.html
##### JVM参数
- 参数类型
  1. 标准参数： 以-开头 如-help，后续版本不会改变
  2. -X参数： 以-X开头 ，如 -Xms最小堆  -Xmx最大堆 -Xss栈大小
  3. -XX参数： 以-XX开头，

## MAVEN
   maven的核心是pom文件.所以只要文件夹里有pom.xml就可以视为一个maven project
   ### 与idea的坑
   idea版本需要与maven版本适应才能在idea中使用,并且新的项目总是使用idea自带的Maven
   ### 配置文件
   repository： 用来指明本地远程库（一个repository代表一个本地远程库）
   mirror: 用来指明下载远程仓库时的镜像
   plugin: maven的生命周期每个周期都是执行相应的插件，plguin可以不指定版本，会下载本地远程库的release版本
   ### dependencyManagement
   用于父pom，对于声明在父pom的该标签下的依赖，子工程可以不写版本号(子工程如果写了以子工程为准),并且父pom不会导入该包
   ### parent & dependency
   dependency标签是parent的子集. 使用parent标签后，子标签除了会import dependency.还会继承一些父类定义的变量值等
   ### 包的管理
   每次导入的就是坐标文件夹下的Jar包.  
   对于import的类文件来说，是没有group与artifity的. 路径就是jar包中的路径.所以可能会存在不同Group或者artifity里面相同路径名称的类，这时候就只能根据在maven里面的依赖顺序决定使用的是哪个类文件
   ### 内部变量
   ${project.version} ： 用在子模块间互相引用时填写在version中
   ### 一些命令行参数
   clean install: 删除target目录，重新生成jar包
   dependency:purge-local-repository：删除repository中该pom的依赖
   nsu： maven的repository中可能有snapshot,默认会在使用时查看远端是否存在最新的，然后更新本地的，加上这个参数会停止这个过程(快照默认每次都会去看有没有最新的 https://blog.csdn.net/weixin_38608626/article/details/88011541)
   -T:  指定线程数
## python
   ### python2/python3
   Python2和Python3分别是Python的两个版本，按照Python官方的计划，Python2只支持到2020年。为了不带入过多的累赘，Python3在设计的时候没有考虑向下相容，许多针对早期Python版本设计的程序都无法在Python3上正常执行 
   ### pip
   pip 是 Python 的包安装程序。其实，pip 就是 Python 标准库中的一个包，只是这个包比较特殊，用它可以来管理 Python 标准库中其他的包
   ### virtualenv
   virtualenv用来建立一个虚拟的python环境，一个专属于项目的python环境,解决了依赖包版本冲突的问题
   会在当前的目录中创建一个文件夹，这是一个独立的python运行环境，包含了Python可执行文件， 以及 pip 库的一份拷贝，这样就能安装其他包了，不过已经安装到系统Python环境中的所有第三方包都不会复制过来，这样，我们就得到了一个不带任何第三方包的“干净”的Python运行环境来
   当import代码时，virtualenv将优先采取本环境中安装的包，而不是系统Python目录中安装的包。

   
## mybatis
   ### retruntype map
   mybatis里当查询到的值用map接收时，key是列名,value是值
   ### 联表查询
   https://blog.csdn.net/codejas/article/details/79532434
   ### 一级缓存
   缓存的单位是session，即一个事务，当遇到增删改自动失效
   ### 二级缓存
   缓存的单位是一个mapper文件，需要实体类实现serizable接口，不可用于分布式


## 前端相关
   ### mdn
   web开发手册，包含js的使用规则等等
   ### DOM与BOM
   BOM是浏览器对象模型，DOM是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作<br /> 
   每个浏览器提供操作dom bom的api<br />
   ### shadow-root
   shadow-root 包裹下的对象，不在全局的dom树中，因此getElementById 等方法，获取不到包裹中的对象。
   该功能的目的就是，独立出一块渲染块，不受外层样式的影响，内层的样式也不影响外层的显示。 
   想要获得的话，访问方式为： 得到shadow-root 外层的根node 这个node是在全局dom树中的。取得gtx的shadow块
   ###  js语法相关
   this: js的this指向调用者(当函数通过xx.func调用时指向xx，直接调用时指向window)
   当函数作为属性时，调用时的this似乎一直跟赋值时的this相等，不会再改变（不确定）
   call()方法： 改变函数的所有者(也可以理解为改变调用时的this)  https://www.w3school.com.cn/js/js_function_call.asp
   js中操作集合，使用foreach前，先想想有没有替代品（foreach能做的事比较多，没法直接看出来要干什么，而some,erery等函数则可以方便看清，并且代码量少）：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
   ### spa应用
   单页面应用，指只有一个页面。 点击页面中的链接不会刷新页面，而是局部刷新组件
   ### webpack与vite 
   两者都是打包工具： 前端写代码时为了方便会将代码写在许多文件中，但是转化成HTML代码时，会使用‘script’标签进行引入js代码，这样会使页面进行的http衍生请求次数的次数增多，页面加载耗能增加。使用打包过后将许多零碎的文件打包成一个整体，页面只需请求一次，js文件中使用模块化互相引用（export、import ），这样能在一定程度上提供页面渲染效率(打包成一个js文件)
   webpack: 分析依赖=> 编译打包=> 交给本地服务器进行渲染。首先分析各个模块之间的依赖，然后进行打包，在启动webpack-dev-server，请求服务器时，直接显示打包结果。webpack打包之后存在的问题：随着模块的增多，会造成打出的 bundle 体积过大，进而会造成热更新速度明显拖慢。(静态编译)
   vite: 启动服务器=> 请求模块时按需动态编译显示。是先启动开发服务器，请求某个模块时再对该模块进行实时编译，因为现代游览器本身支持ES-Module，所以会自动向依赖的Module发出请求。所以vite就将开发环境下的模块文件作为浏览器的执行文件，而不是像webpack进行打包后交给本地服务器。(动态编译)

   ### 验证input输入完成
   一般可以用onblur方法，既失焦时触发

   ### node.js
   每个浏览器都有自己的解释引擎，所以可以识别js代码<br /> 
   node.js可以让js代码做后端开发。本质是js的运行环境.通过  node js路径  指向js文件<br /> 
   内置模块fs,path,http等，模块的本质就是js文件<br /> 
   module:自定义模块的全局对象，当别的模块通过require引入其他模块时，实际就是获得该模块的module.export对象(为了书写方便，export和module.export等价)<br /> 

   ### npm
   包管理器(既模块)<br /> 
    npm init     项目初始化，会出现三个文件   node_module:存放第三方包   packgae.json:类似于Pom文件   package-lock.json:是用来固定版本的<br /> 
    npm i == npm install   <br /> 
    npm i 包名@版本   版本号由三位组成  第一位代表大版本，一般是重构或大改动时改变    第二位是功能版本号，有新功能时修改    第三位是bug修复版本号<br /> 
    npm i 包名 -D = npm install 包名 --save-dev    会将依赖记录在devDependencies里面，而不是普通的dependencies<br /> 
   
   ### yarn
   Yarn是由Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具 ，正如官方文档中写的，Yarn 是为了弥补 npm 的一些缺陷而出现的。<br /> 
   ### ES6
   es类似于js中jdk版本的存在
   一些es6语法规范： https://www.jianshu.com/p/7c35993b7bb3
   ### commonjs,ES6,import和require
   commonjs和es6是两个关于模块化的标准  ：https://www.jianshu.com/p/58f49f69a2fb	<br /> 
   ES6标准发布后，module成为标准，标准使用是以export指令导出接口，以import引入模块。import和export时都是到node_module文件夹中<br /> 
   ### 语法糖
   用更简练的言语表达较复杂的含义。在得到广泛接受的情况之下，可以提升交流的效率。
   ### 定时器
   setinterval(function,time)   启动一个定时器，定时执行。 一般需要在创建时接收对象，使用clearInterval清除定时器
   ### prototype、__proto__与constructor
   实例和原型是两个相反的概念  <br />
   https://blog.csdn.net/cc18868876837/article/details/81211729   图片 <br />
   https://zhuanlan.zhihu.com/p/130503924 <br />
   student.__proto__ === Student.prototype <br />
   __proto__:    __proto__指向了实例对象的原型对象；当你访问一个对象上没有的属性时，对象就会去__proto__上面找，如果还是找不到，就会继续找原型对象的__proto__，直到原型对象为null；因此__proto__构成了一条原型链。<br />
   prototype:   prototype是从一个函数指向一个对象，即函数才有prototype属性。这个函数所创建的实例的原型对象.它的作用是让该构造函数创建的所有实例对象们都能找到公用的属性和方法。任何函数在创建实例对象的时候，其实会关联该函数的prototype对象<br />
   constructor:  constructor属性也是对象才拥有的，它是从一个对象指向一个函数，含义就是指向该对象的构造函数 <br />
   把方法写在构造函数的内部，增加了通过构造函数初始化一个对象的成本（内存占用，因为两个实例对象就创建了两个一样的方法），把方法写在prototype属性上就有效的减少了这种成本<br />
   属性写在实例里，方法写在原型
  ### 箭头函数和普通函数区别
   箭头函数的this是不变的，指向**定义**时的this. 普通函数的this是随着调用者改变的(例：var a =  (1) => {this.xx} this为1对应处的this,如果1不在一个大括号里面，说明没有作用域，则是指向window 而 var a = function ppp((1) => {this.xx}) 则是有作用域的，this就不是window了  既判断第一个括号是否在函数中)
   https://blog.csdn.net/qq_43303102/article/details/113005871
   ### promise<br /> 
    类似于java中的callable接口，用于异步调用  https://www.cnblogs.com/superSmile/p/8406037.html
   ### 属性的赋值
   属性的赋值有两种方式： obj.name='xiao'  obj[name] ='xiao'
   object[key]=>key为常量时，object[key]等价于object.key，例如：a.b == a['b']
   特殊的，object[key]=>key为变量时，只能用中括号形式
   ### typescript
   - 简介
   typescipt是以js为基础的语言，扩展了ts,ts实际是编译以后生成js代码.
   - ts中的类型
   ts类型除了普通的boolean,string等，还可以为字面量，既某个具体的值  let a = "male" | "female"
   除此之外还可以为any,但是一般不建议设置成any,可以设置为unknow. any与unknow的主要区别就是能不能给其他属性赋值(any可以把这个变量的值赋给任何变量，unknow声明的则不可以)
   还可以通过{filedName: type} 来声明一个指定属性的object (如果要动态属性的话需要复杂一点)
   [typeName, typeName...] 这个代表一个元组,固定长度的数组
   type typeName = {...}  给右边的类型起一个别名

   ### react
   将数据渲染成视图的工具<br /> 
   传统的操作dom会造成浏览器多次渲染，效率低<br /> 
   react采用组件化模式，声明式编码，以及虚拟dom,减少与真实dom的交互(可以实现dom复用等功能).虚拟dom的本质是个object<br />
   react生成li标签时，建议携带唯一的key<br />
  - 教程<br />
    https://www.bilibili.com/video/BV1wy4y1D7JT?p=95<br />
  - react rule
    react给form添加规则时，不要通过绑定事件然后在方法中判断是否成功，而是可以通过rule属性来进行处理  
  - 在父组件获取子组件的的state
    signoffModal: RefObject<SignoffModal> = React.createRef();  
    <SignoffModal    ref={this.signoffModal}  />
    let modal = this.signoffModal.current
  - 在子组件修改父组件pros或者state
    可以将父组件修改的方法传入子组件  
  - babel<br /> 
    将jsx转换为js<br />
  - jsx<br /> 
    jsx可以理解为类似于xml的js语法，是render函数中使用的语法。它与js有一些小的语法区别   https://www.bilibili.com/video/BV1wy4y1D7JT?p=5
    其中一个规则是组件名称开头要大写
    react中的虚拟节点中，可以使用表达式（表达式与语句的区别： https://www.bilibili.com/video/BV1wy4y1D7JT?p=6   最简单的区别就是有无返回值）
  - react组件<br /> 
    实现局部功能效果的代码和资源的集合 。react中的组件化，把一个页面的区域分成几个部分，每个区域用一个组件表示。分为函数式组件和类式组件<br /> 
  - 函数组件<br /> 
    通过function xxx(){return xxx} 定义, 函数组件中的this是window
  - 类组件  <br />
    class xxx extends React.Components(){render() {} }      必须有render函数。class中的this指向实例对象
  - 周期函数
    周期函数中的mount代表的是组件mount到节点上
    初始周期： constructor----willmount-----render-----didmount
    更新周期：（触发点1  父组件修改props）-------willreceiveProps------(触发点2 setState)-----shouldUpdate(返回boolean，类似拦截器)-----（触发点3 forceupdate）-------willUpdate----render-----Didupdate
    新版本中与will相关的生命周期都不推荐使用了  （可以通过比较props和prepros来进行不同用途的生命周期）
    getderivedStateFromProps  使state永远从props获取  （基本不用）
    getSnapshotOfState(更新时使用，将返回值传给didUpdate)
  - state <br/>
    数据存放在state中，state用来驱动页面。通过构造函数初始化<br/>
    如果一个组件有state,就是复杂组件。<br/>
    函数组件不能携带state.<br/>
  - props<br/>
    用于在创建组件时传值。 props是只读的 <br/>
    函数组件也可以使用props. 在函数内部通过const去接收props的值 <br/>
  - refs<br/>
    组件实例拥有ref属性。 <br/>
     由于react不操作dom,所以用ref来获得某个标签（可以理解为id）,使用ref获得的dom是真实dom<br/>
     有三种使用方式：  1. 字符串类型  ref="input1" （效率比较低，已不推荐使用）  2.  回调函数形式  ref= (currentNode) => this.input1 = currentNode  (将真实dom绑定到this的某个属性上，由React自己调用，但是当重新渲染时，会调用两次该方法)  3.  createRef法：  a = React.createRef  然后将ref = a
     尽量不要写ref,比如同一个input上，需要在事件时获取自己的值，可以在event中取到<br/>
  - 事件绑定  <br />
    react事件绑定相当于一个中间变量，所以需用箭头函数或者bind方法
    绑定事件时要写方法名，不要携带括号。携带括号意味调用函数，也就是把函数的值返回<br/>
    有括号, 函数会立即执行, 然后返回结果;
    无括号, 会将函数 作为"对象"赋值给你的变量 .
  -  react构造函数<br/>
    主要做一件事： 给state设置初始值；  但是如果写了构造函数，要记得写super(props)<br/>
  -  react-creator脚手架<br/>
    帮助你快速新建一个项目<br/>
    初始构建好有以下文件夹：  node_modules, public(存放静态文件,内含index.html，是react项目唯一的html文件),src(js文件等)<br/>
  - proxy<br/>
     1.   在package.json中配置proxy,改变请求的指向（将前端的localhost:3000(启动端口)的请求指向某个url，主要是为了解决跨域问题） 缺点：只能配一个proxy<br/>
     2.   如果需要配置多个proxy的话，可以用middleware<br/>
  - react路由<br/>
     路由就是key-value的关系，不同的path对应不同的组件或函数<br/>
     <Redirect to={{ pathname: '/login', state(自定义属性): { from: this.props.location } }} />  路由信息存在this.props.location中. 通过浏览器访问时会自动填充pathname属性
     原理是bom中含有hisyory属性，是一个栈，history.push会改变path。然后可以给这个栈设置监听事件<br/>
     通过react-router插件实现<br/>
  - hook
     在函数式组件中是不能使用state,周期函数等概念的，但是可以通过hook实现类似效果<br/>
     useState: 返回一个state，以及更新state的函数  https://blog.csdn.net/wu_xianqiang/article/details/105181044   useState有一个坑，React 官方文档提到：组件内部的任何函数，包括事件处理函数和 Effect，都是从它被创建的那次渲染中被「看到」的，所以引用的值任然是旧的，最后导致 setState 出现异常  https://www.cnblogs.com/hymenhan/p/14991789.html
     useEffect： 类似于周期函数  https://www.jianshu.com/p/6e525c3686ab
     useRef:  类似于REF  https://blog.csdn.net/hjc256/article/details/102587037
  - UI框架
     antd  蚂蚁出品<br/>
     antd的form有个坑，input的name需要绑定类的属性，对这个属性的赋值才能生效
   ### 静态页面，动态页面
   静态页面一般可以跟文件类似，通过url直接访问<br />
   静态资源：可以理解为前端的固定页面，这里面包含HTML、CSS、JS、图片等等，不需要查数据库也不需要程序处理，直接就能够显示的页面，如果想修改内容则必须修改页面，但是访问效率相当高。<br />
   动态资源：需要程序处理或者从数据库中读数据，能够根据不同的条件在页面显示不同的数据，内容更新不需要修改页面但是访问速度不及静态页面。<br />
   
   ### 跨域问题，cors
   只要协议，域名，端口号，有一个不一样，就会产生跨域问题（websockect协议不会产生跨域问题）<br />
   通常可以通过cors或者jsonp两个办法绕开跨域（jsonp由于只能用于get请求等原因，已经弃用）<br />
   cors通过给被调用方response的head中添加Access-Control-Allow-Origin 等字段允许跨域访问（如果response中没有这个头，浏览器会拦截这个数据，所以也可以通过在浏览器端配置跨域使跨域生效）<br />
   cors请求的类型： https://www.bilibili.com/video/BV1a34y167AZ?p=55<br />

   ### express
   一个基于Nodejs的http包，可以轻松的实现api服务器，和静态服务器的功能 （静态服务器既将html,css等允许直接访问）  <br />
   url中，localhost:8080/usr?name=10  这种查询，叫做query式url   localhost:8080/10   这种叫做param式<br />
   express中的路由是模块化的。既一个路由是由多个js文件注册在一起的。<br />
   express中有一个中间件的概念： 一个req,res可以由多个函数处理，这里的处理函数就叫做中间件<br />

    ### nodemon
    一个热重启的插件，使用nodemon xx.js  启动js文件，可以在保存后自动重启项目<br />
   
   ### eslint
   是一个第三方插件，用来查看前端代码不规范的地方   使用方法：https://blog.csdn.net/guang_s/article/details/90231312<br />
   ### prettier
   ### this
   this有显示绑定，隐式绑定等概念，在react中使用时会涉及到bind等行为 https://www.cnblogs.com/DM428/p/7777539.html    
   怎么写bind比较优雅   https://blog.csdn.net/flytam/article/details/104760202  
   ### package.json与package-lock.json
   package.json类似于pom文件，package-lock是用来锁定版本号的
   在npm install时，如果lock与packgae版本兼容，则依据lock.不兼容则更新lock
## 计算机网络
   ### 网络安全
   #### ddos
   http://www.ruanyifeng.com/blog/2018/06/ddos.html
   #### 公钥与私钥
   公钥用于加密，私钥用于解密
   #### 证书
   颁发的证书一般有三部分： 公钥，私钥，证书，其中证书一般与公钥是在一起的
   颁发的私钥一般是加密的，需要解密后才可以使用
   #### ssl过程
   完成时为对称加密的形式(客户端与服务端共用一个key进行数据传输)
   https://www.cnblogs.com/hld123/p/15255526.html

   双向验证： https://www.jianshu.com/p/fb5fe0165ef2
   #### hsts
   浏览器维护一个hsts表，在表中的网站只使用https的方式连接，拒绝所有http请求
   
   ### vpn与proxy
   https://zhuanlan.zhihu.com/p/451193697
   vpn与proxy都是服务器，vpn需要下载软件，与vpn服务器形成隧道传输，比proxy多了加密功能
   
   ### ping
   ping使用icmp协议，不携带端口号，可以关闭电脑的ping功能
   
   ### htpp请求
   #### time_wait
   在四次挥手中，客户端最后需要有一个time_wait的时间，以确保没有包存活。而这个time_wait对于高并发的时候则是很吃力的，所以对于高访问的机器可以适当调低，或者尝试使用长连接来减少连接数量<br/>
   netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'   查看数量<br/>
   #### keepalive_timeout
   传统的http请求都是在完成一次发送后结束连接，当指定了keepalive_timeout时，会在每次发送后开启计时，达到时间才关闭连接
   #### Cache-Control
   位于response header中，用来向客户端声明资源的有效时间(浏览器默认只有刷新才会去重新刷新资源，关闭重进并不会自动刷新)
   https://blog.csdn.net/ljfrocky/article/details/123032502
## 操作系统
   ### 并发与并行
   并发是指一个处理器同时处理多个任务。
   并行是指多个处理器或者是多核的处理器同时处理多个不同的任务。   

## Redis
   ### 默认配置
   redis默认的内存是0，既无上限。默认清除策略是不清除。所以要设置过期时间
   过期时间的最小单位是key,对于map,list等结构，一次清除，全部清除（redisson中具有实现value过期的map）
   ### redission使用手册
   https://www.bookstack.cn/read/redisson-wiki-zh

## zookeeper
   ### 节点类型
   持久节点：该数据节点被创建后，就会一直存在于zookeeper服务器上，直到有删除操作来主动删除这个节点。
   临时节点：临时节点的生命周期和客户端会话绑定在一起，客户端会话失效，则这个节点就会被自动清除。   

## ELK
   ELK是三个开源软件的缩写，分别表示：Elasticsearch , Logstash, Kibana(由于后面又有一些新的组件加入，所以又称为elasticStack es)
   logstash收集信息 ----》es数据库 -----》kibana数据展示
   ### elasticsearch
   #### 简介
   Elasticsearch是个开源分布式搜索引擎，提供搜集、分析、存储数据三大功能。它的特点有：分布式，零配置，自动发现，索引自动分片，索引副本机制，restful风格接口，多数据源，自动搜索负载等,9200为服务端口，9300为通信端口
   主要通过http请求进行操作，是由lucene封装而来
   #### 概念
   index: 等同于mysql中的数据库
   type: 可以理解为表，不过已经弃用，因为同一索引数据都是在一起的，不同type之间如果属性不同会造成大量空值
   document: es中的最小单位，可以理解为一行，是jason格式存储的
   field: 相当于列，指定一个document应该有哪些字段
   shard: 分片，将数据分片存储在多台机器上,默认为1
   replica: 副本，既主备，默认为1
   #### 集群
   一台机器可以有多个主分片
   同一索引同一分片的主分片与副本分片不能在一台机器上，且一个索引的主分片数量是固定的，副本分片是可以改变的。
   当主分片挂了，会查看有没有对应的副本分片，如果有的话就转为主分片，没有就宕掉了
   如果是集群环境es会自动把主分片分到不同的机器上（比如两个节点时，两个主分片会在一台机器上，另一台上放对应的副本分片）
   #### 状态
   绿色：所有主分片和副本分片可用
   黄色：存在副本分片不可以，所以主分片可用
   红色：存在主分片不可用
   #### TF/IDF算法
   一个词语在一篇文章中出现次数越多, 同时在所有文档中出现次数越少, 越能够代表该文章
   Term Frequency: 判断搜索的关键字在文章中出现的次数，越多则相关度越高
   Inverse Document Frequency： 判断某个搜索的关键字在所有文章中的出现次数，出现次数越多，该关键字的相关度就越低
   最终的结果为TF*IDF
   #### crud操作
   新建索引: PUT /indexName
   新建document: POST/PUT /indexName/type/(表名，以后会启用 一般写 _doc)/id/_create  {json串}，也可以不指定id,自定生成id
   获取document: 1.全局返回：GET /indexName/type/id   2.返回指定field  GET /indexName/type/id?_source_indludes=fielName1,fieldName2
   更新document: 1.全局替换：  POST/PUT /indexName/type/id  {json串}   2.局部更新： POST /indexName/type/id/_update {"doc":{json串}}
   批量操作: bulk (推荐使用\n进行分行，因为可以减少服务端进行Json->jsonArrray的转换)
   #### 指定搜索
   indexName/_search?q=(+-)fieldName:xxx  指定关键词搜索  -号代表不含有xxx
   indexName/_search?q=sort=fieldNam(:desc) 根据某一列排序
   indexName/_search?timeout=10ms 指定搜索的最长等待时间(在这个时间内，搜到多少条就返回多少条)
   indexName1,indexName2/_search 多index搜索
   indexName/_search?from=x&size=y 分页查询,返回第x 起的y条数据(默认根据相关度排序)  当from数量太大时，会出现deep paging问题(因为分布式时，会去所有子节点取出x+y条数据，然后再排一次序，造成消耗带宽等问题) https://www.cnblogs.com/michael9/p/14632698.html
   以上这些参数都可以通过body携带

   filter: 查询结果中必须要包含的内容，不会影响相关度
   should: 查询结果非必须包含项，包含了会提高分数，影响相关度
   must_not: 查询结果中不能包含的内容，不会影响相关度 可见，filter 和 must _not 单纯只用于过滤文档，而它们对文档相关度没有 任何影响。换句话说，这两种子句对查询结果的排序没有作用。在这四种子句中， should 子句的情况有些复杂。首先它的执行结果影响相关度，但在是否过滤结 果上则取决于上下文。当 should 子句与 must 子句或 filter 子句同时出现在子句 中时，should 子句将不会过滤结果。也就是说，在这种情况下，即使 should 子 句不满足，结果也会返回

   #### mapping
   在创建index时可以对document的属性类型进行设置，如果不指定则会根据字段值进行动态判断。(不同类型的属性查找规则不同,有些是全文检索，有些是精确匹配)
   Get indexName/_mapping 查看一个索引的映射
   PUT indexName/_mapping {"properties": {json}}  创建某个index的索引
   在给一个index设置type时，可以指定dynamic mapping配置(开启、禁用、不设置索引)
   ##### 类型
   text: 文本类型，可以添加参数来设置某个属性使用的分词器、是否需要建立倒排索引(默认是不支持排序的，因为倒排索引后不知道原数据的组成顺序)
   keyword: 关键词类型，与text类似，但是不建立倒排索引(index:false)
   date:不需要设置分词器，可以定义存储的日期的格式
   数值类型: byte、int、float等(还有一个scared_float,是指把小数类型作为整数存储)
   ##### 自定义动态索引
   可以自己定义动态索引的设置规则，让某些field匹配为某种type. 比如按照field名称的正则匹配等等
   ##### 修改mapping
   如果索引已经插入数据，则映射无法修改，只能删除索引重新创建，所以创建索引后就要指定mapping类型。 
   修改的话通常是新建一个index,然后type改好，把原index的数据全部导入新的索引
   #### 倒排索引
   es维护一个倒排表，将单词和对应的document进行一个连接，同时把该单词进行一个同义词/时态的转化(一个Index的一个filed就对应一个倒排表)
   #### 分词器
   将一段文本通过分词器处理，然后存入倒排表中(可以自己配置很多参数)。
   存储的时候使用一个分词器，对该属性搜索的时候用另一个分词器(搜索的时候如果是全文索引，也会对搜索的内容进行分词)，一般来说存储用分成最多数量的分词，搜索用分成最小数量的
   默认有五种分词器
   使用GET /_anaylize 来测试分词器工作结果
   ##### ik分词器
   中文分词器
   大概有27w个分词
   可以添加自己的分词，可以加在mysql里也可以加在文件里
   ##### 工作步骤
   1.character filter 
   常见的如：去掉一些<html>等无效字符 ,将&转换为and等
   2.tokenlizer
   把句子化为一个个单词
   3.tokenfilter
   常见的如：去掉一些语气词(a,the,an等,默认不去掉)  ，转换为小写
   #### 存储选择原理
   通过对document进行hash计算取模，决定放在哪个主分片
   #### 替换与删除原理
   替换时更新version版本(局部更新也会更新version)，旧的version并不会马上删除，而是在一个时间一起删除。 
   删除也不会马上删除，会先标记，等待时间再删除(为了减少io访问次数)
   #### 内置脚本
   ```
      POST /book/_doc/1/_update 
         {
         "script":"ctx._source.price+=1"
         }
   ```
   #### 乐观锁机制
   java中可以在请求中携带version来使用乐观锁机制(也可以设置VersionType.EXTERNAL，只要当前的版本号高于es中的版本号，就可以存入)

   ### kibana
   #### 简介
   是用来图形化查看es的工具。默认端口5601 

   ### logstash  
   #### 简介
   数据收集工具，将某个地方的数据存入另一个地方(比如mysql的存入es)
   #### 组成
   input ----> filter(可以将input的数据按照正则解析为很多个字段) ----> output


## tomcat
   ### catalina.out
   catalina.out用来存储控制台打印的信息即标准输入的目的地,在log4j中配置的consoleappender也会输入到此. 一般都含有gc信息（jdk默认在gc时会向控制台输出信息，可以通过jvm potion关闭）
   ### CATALINA_BASE和CATALINA_HOME
   当一台机器上有多个app,不想都放到webapp目录下时(如果都在webapp会造成无法单独启动的问题)，可以给每个app设置单独的CATALINA_BASE(简单理解为属于app自己的一个tomcat环境)，然后把tomcat根目录的log文件夹copy过去，创建bin目录以及start.sh/shutdown.sh,即可直接在app目录启动自身

## postman
   ### basic auth
   basic auth实质就是在header里添加("authorization" , "Basic (name:password).toBase64")   


## restful
   ### 请求类型
   get: 查    post:新增(非幂等)   put:更新所有  patch:更新某个属性(非幂等，因为可能导致update_time字段改变)  delete:删除
   head： 只返回相应的head信息，不返回body
   ### 规则
   url中只存在名词，不存在动词，并且最好与数据库的表名对应


## graph ql
   是一种来替代restful api的技术，查询时可以指定需要查询的属性
   一般只有一个post api  
   {
      operation(query,mutation) {
         endpoint(user) {
            field1 (name)
            field2 (age)
         }
      }
   } 

## osgi
   是一种实现模块化的框架. OSGi 是严格要求模块化的，模块有个专有名词 bundle。每个模块都是一个 bundle，一个 Business Logic 由多个 bundle 来实现
   当一个 bundle 发现并开始使用 OSGi 中的一个服务了以后，这个服务可能在任何的时候改变或者是消失。
   SOA粗暴理解：把系统按照实际业务，拆分成刚刚好大小的、合适的、独立部署的模块，每个模块之间相互独立。

## keystore
Keytool 是一个JAVA环境下的安全钥匙与证书的管理工具，Keytool将密钥（key）和证书（certificates）存在一个称为keystore 的文件(受密码保护)中。keystore生成时自带证书，只能先删除原有的。
.p12文件是用来给keystore使用的，由证书和私钥生成
openssl pkcs12 -export -in cert.pem -inkey key.pem -out cacert.p12
keytool -importkeystore -destkeystore /opt/fastrun.app/conf/tomcat.keystore -srckeystore cacert.p12 -srcstoretype pkcs12
keytool -importkeystore -destkeystore /opt/fastrun.app/conf/ca -srckeystore cacert.p12 -srcstoretype pkcs12   
还有个类似的文件时.jks文件，这个文件是通过Android studio生成的，本质跟.keystore文件一样
一个keystore可以存多个privatekey-cert组合，但是不建议这么做

   
## truststore
   在java的jre\lib\security 文件夹下有一个cacerts文件，也被称作truststore,是用来存放受信任的证书的



## mysql
   ### 5.7安装
   分为免安装版和安装版，免安装版教程：https://www.cnblogs.com/itcui/p/15511683.html   网址：http://ftp.ntu.edu.tw/MySQL/Downloads/MySQL-5.7/   
   ### char比较时的坑
   对于值为null的char,任何判断都会为false. 例如 name != 'a',是不会包含name为null的数据的，需要在前面加上is null包含上null的数据
   ### having与where
   https://blog.csdn.net/qq_37189082/article/details/122607549
   where作用于表数据过滤，Having作用于组数据的过滤；where在分组和聚合之前选取数据，having在分组和聚合之后选取分组数据
   ### like
   like默认是不区分大小写的
   ### 配置文件
   ["client"]
   socket =xxxx  来指定客户端使用的socket文件
   ### 数据类型
    #### unsigned
    无符号类型
   ### log类型
   https://zhuanlan.zhihu.com/p/213770128
   binlog: 存储所执行的sql语句
   redolog: 与事务相关，保证事务的一致性。与Binlog类似。但是粒度比binlog小，记载的是对页的操作 （binlog只有在事务结束提交前写入一次，但是redolog则是在事务过程中不断添加，所以可恢复成度也大于binlog）
   undolog: 主要保证回滚的正确性，通过一个指针串联起一行数据的多个版本
   更多redolog和binlog区别： https://blog.csdn.net/weixin_44691915/article/details/122860263
   ### 索引
    #### 索引失效
    https://www.cnblogs.com/wdss/p/11186411.html
   

## druid
   连接池技术，是目前最快的连接池
   Druid连接池是阿里巴巴开源的数据库连接池项目。Druid连接池为监控而生，内置强大的监控功能，监控特性不影响性能。功能强大，能防SQL注入，内置Loging能诊断Hack应用行为

## nginx
   ### 反向代理与正向代理
   最主要的区别是被代理的对象，如果被代理的是服务器，则是反向代理，被代理的是用户，则是正向代理   

## jmeter
   ### ramp-up
   ramp up的值应该是启动全部线程所需的时间   

## log4j
   ### 日志级别
   debug < info < warn < error
   ### DailyRollingFileAppender
   按天生成日志文件，旧的log会带后缀

## lombok
   ### 使用
   项目需要下载lombok的依赖，idea需要下载lombok插件

## mycat
   一款可以分库分表的数据库中间件，但是已经不在维护，不推荐使用   

## 代码测试
   阶段： 单元测试 ---->  集成测试  ----->  系统测试
   集成测试和系统测试区别不大
   冒烟测试(smoke test): 冒烟测试这个名称的来历，最初是从电路板测试得来的。因为当电路板做好以后，首先会加电测试，如果板子没有冒烟再进行其它测试，否则就必须重新来过. 冒烟只是这类测试活动更形象化一些的叫法，目的是保证系统基本功能可用   
   回归测试(regression): 当修复一个BUG后，把之前的测试用例在新的代码下进行再次测试。 确保改完原来的BUG后，没有给其他部分带来新的缺陷
   BVT(Build Verification Test): 主要目的是验证最新生成的软件版本在功能上是否完整，主要的软件特性是否正确。如无大的问题，就可以进行相应的功能测试（bvt与smoke test差不多）

## testng
   一款基于junit的自动化测试框架
   listener类可以继承,如果继承了多个listner(多级关系),那么不同参数相同注解的方法会都执行
   @Test 注解一个test方法
   @Before/After Method修饰的方法可以携带参数 Method method, ITestResult result，
   
## harbor
   docker的本地镜像仓库,提供了ui操作

## k8s
   ### 简介   
   google开源的容器管理技术
   ### 组成
   由master和node节点组成
   ### 安装
   机器初始化(关闭防火墙，禁止swap分区等). 安装docker,kubelet,kubeadmin,kubectl.  kubeadmin init

   #### master
   ##### ApiServer
   集群的统一入口，以restful方式进行请求，然后交给etcd处理
   ##### scheduler
   调度器，决定在哪个node上面进行部署
   ##### controller-manager
   对某个资源进行控制(比如有多个订单服务pod，那么由一个订单服务manager来管理)
   ##### etcd
   可以理解为数据库，存放数据

   #### node
   ##### kubelete
   master放置在node上的一个agent,用来获取node上的运行情况等
   ##### kube-proxy
   用于网络代理

   ### 概念
   #### pod
   最小部署单元，由一个或多个container组成. 内部的网络是共享的. pod是短暂的
   创建pod时先创建一个pause容器，然后把业务容器加到pause容器中，由此实现网络共享
   使用volumn来进行数据的共享存储
   创建pod时需要指定controller与service类型
   #### controller
   控制pod的创建和销毁. controller和pod通过label关联 . 常见的控制器类型有deployment、Job 、statefulset 、daemonset 等等。
   deployment 是最常见的controller，它是部署静态服务用的控制器。控制器是通过标签来关联查找pod 的
   #### service
   可以理解为注册中心,pod创建时需要将自己注册到service. 同时还会给pod集群做负载均衡
   clusterIP: 只允许集群内部间访问
   NodePort: 可以允许外部访问
   loadbalance: 
   #### 镜像策略
   镜像拉取策略:  根据宿主机有无该image 分为三种
   资源限制: 可以设定满足条件的机器才会启动某个镜像
   重启策略: 当容器关闭时，是否自动启动等
   #### probe
   https://blog.csdn.net/fastrunner2003/article/details/123676828
   针对的对象为container，可以根据http请求的返回值，也可以根据执行命令的返回值来判断是否存活
   livenessprobe: 如果返回为错误，则会重启container(同时pod状态也是不能服务的)
   readinessprobe: 如果返回为错误，pod不会对外提供服务，也就是无法访问这个pod(挂掉的话不会自动去重启)
 
   ### k8s yaml文件
   实际生产环境中使用yum来操作k8s
   yum文件的内容分成两部分： 控制器定义，pod信息 (两部分一般由templete字段来区分，上面的是控制器定义，下面的是pod信息)
   创建yum文件的方法： kubectl create deployment --image=nginx -o yaml --dry-run


   ### 命令
   #### kubectrl
   k8s的命令行操作，创建pod等等操作

   #### labels
   kubectrl label 可以给node/pod/servcie 打上key-value键值对

   #### create
   kubectl create 用来创建pod

   #### expose
   kubectl expose rc nginx --port=80 --target-port=8000    将pod端口暴露
   port代表在集群内布供其他pod访问的端口. --target-port表示该pod需要被暴露的端口

   #### set image
   进行版本升级
   kubectl set image  修改某个controller或者某个pod的镜像版本(会新建一个新的pod,当准备就绪后关闭旧的pod,启用新的)

   #### rollout
   kubectl rollout 回滚版本   (options)
   undo  回滚，   history历史

   #### scale
   kubectl scale 弹性伸缩

   
   

## DGS graphql
   一款用于实现graphql的java框架
   使用时在resource文件夹中创建schema文件，来指定返回值的类型。
   通过@DGSComponent注解声明一个fetcher,一般一个返回值对应一个同名方法 通过配置resolver来进行分表查询
   自带一个前端页面来方便进行graphql查询  
## spring
   ### spring3
   无法在spring3中使用lmbda
   ### requestmapping
   在spring4中引入了@getmapping,@postmapping注解，用来表示指定类型的请求(requestmapping默认接受任何类型) 
   ### 创建多模块
   多模块时需要选取一个父模块来控制依赖版本，以及一个模块来存储公共的实体类和工具类  
   ### spring生命周期
   实例化 Instantiation
   属性赋值 Populate
   初始化 Initialization
   销毁 Destruction
   ### 一些常用注解
   @PostConstruct： 用于注解在init方法上，在赋值后执行
   @configuration:  用来表明该类有bean的创建
   @PathVariable: 例如/blogs/1
   @RequestParam，例如blogs?blogId=1
## springboot
   ### yml配置
   一定要注意空格关系！！！！
   注意： datasource配置是属于spring一级的  
   ### 新建项目步骤
   建module,改pom,建yml,启动类，主代码
   注意：如果不需要数据库操作，不要导入mysql相关包，会报错的
   ### 简单的集群项目
   直接修改port再重启一次即可  

   
    
## springcloud
   https://yunyanchengyu.blog.csdn.net/?type=blog
   ### 与dubbo关系
   springcloud是在dubbo的基础上建立的，后来又被spring-alibaba包含
   ### 版本
   springcloud版本以英文字母命名A-Z ,与springboot会有版本依赖
   ### bootstrap.yml
   bootstrap.yml（bootstrap.properties）用来在程序引导时执行，应用于更加早期配置信息读取，如可以使用来配置application.yml中使用到参数等
   application.yml（application.properties) 应用程序特有配置信息，可以用来配置后续各个模块中需使用的公共参数等。
   bootstrap.yml 先于 application.yml 加载且不会被application.yml覆盖
   ### 服务注册中心
   #### 简介
   将provider和counsumer注册的地方
   #### 调用
   注册进以后客户端直接通过服务名称访问生产者：  http://CLOUD-PAYMENT-SERVICE<br/>
   被注册后依然可以使用ip进行访问
   #### eureka
   需要一个模块来启动eureka服务，无需下载，导入pom启动即可<br/>
   服务端启动类注解@enableEurekaServer  ,注册端加@enableEurekaClient注解<br/>
   最好使用eureka集群，集群server之间相互注册, client里任写一个server就行<br/>
   服务发现： 可以发现服务的信息（端口，ip等等）<br/>
   保护模式： eurake属于ap类（高可用），不会自动清除微服务。短时间内大部分客户端丢失时，会进入保护模式。（好死不如赖活着）。默认开启，可以在配置文件关闭<br/>
   #### zookeeper
   直接在客户端指明spring cloud里面的zk地址即可，不需要新的模块启动zk服务端
   ### 服务调用
   #### resttemplete
   主要有两个方法: getObject和getEntity 一个是返回body,一个是加上返回状态码请求头等详细信息
   在springcloud 的使用中如果使用RestTemplate来进行rpc远程调用的时候 ，在调用服务的时候有的会选择使用服务端在注册中心注册的名称来进行远程调用 也有的会直接使用域名进行调用，在这个过程中如果使用注册名称的话在RestTemplate 那里开启 负载均衡 :  @LoadBalanced  如果是使用域名进行调用就不用开启负载均衡 
   #### ribbon 
   **客户端负载均衡**，由客户端选择访问哪台服务器
   可以理解为 带负载均衡功能的resttempletea（实际使用时也是跟resttemplete一起使用）
   @LoadBalanced既是调用了ribbon的负载均衡
   默认是ZoneAwareLoadBalancer(轮询策略的一种升级)，可以根据不同的微服务选择不同的策略，也可以全局配置统一的策略（配置后直接作用于所有相关url的请求）
   也可以自己实现一个负载均衡算法，核心是重写chose方法和lb的getserver方法
   #### openfeign
   使用注解形式完成http请求,本质还是resttemplete（负载均衡也是使用的ribbon）
   https://blog.csdn.net/manzhizhen/article/details/110013311
   与springcloud整合时，默认携带1s超时时间
   requestInterceptor(new BasicAuthRequestInterceptor(userName, password)) 会作用于所有请求
   openfeign默认的解码器只支持String类型、[byte]类型。 与springcloud整合时会调用Spring MVC 中的消息转换器（HttpMessageConverter）进行编码，而消息转换器适配了很多种数据格式，String、Byte、Json、XML都是支持的。
   当使用参数作为path一部分时，要注意对参数进行urlencoder(默认会把所以%2F转换成/，如果不需要可以通过decodeSlash = false 关闭这个功能)
   ### 服务容错
   #### Hystrix
   是一个用于处理分布式延迟和容错的第三方库，保证在单个应用出错的情况下，不会导致整个服务失败，避免级联故障
   主要功能： 降级，熔断，限流，监控 
   ##### 降级（fallback)
   当服务不可用时，返回友好的信息  (不可用包括 抛异常，超时等)，一般写在客户端(早发现早治理)
   @HystrixCommand(fallbackMethod = "paymentInfoTimeOutHandler", commandProperties = {
            @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "5000")
    })
   注解加在服务上，指定降级要调用的方法 (降级的调用方法需要与被降级方法同类型参同类型返回值)
   @EnableHystrix  加在启动类上

   一般设置一个默认的降级方法（该方法没有参数）
   ##### 熔断(break)   : 
   当一段时间内调用都失败时，拒绝访问，调用降级方法.过一段时间后自行恢复 (可以理解为保险丝，与降级相比多了个时间维度，且一般设置在服务端)
   @HystrixProperty（name = "xxx", value ="xx"）填写触发熔断的条件(多少次请求失败啦，失败后的重试时间是多少等)
   ##### 限流(limit) :  当一定时间访问量过大时，排队访问
   ##### 监控
   可以设置dashbord监控hystrix相关的服务，dashbord本身也是个模块
   ### 服务网关
   网关是微服务的入口，nginx的流量打到网关（网关其实就类似于一个nginx模块，但是功能比nginx多，可以额外做权限啦之类的事情）
   #### gateway
   基于netty实现的，非阻塞,支持websocket
   路由： URL
   断言： 指请求头中的参数，url路径等，还可以设置before after来进行时间相关的限制，设置是否携带某个cookie
   过滤： 过滤器,主要是用来给修饰请求的，一般是实现自定义的（给请求头添加点东西之类的或者自己对请求做一些判断等）
   核心： 路由转发+执行过滤链
   与ribbon的区别是ribbon是客户端负载均衡，而gateway是服务端实现
   ### 服务配置
   #### spring-cloud-config
   用来统一管理配置文件的地方，提供中心化的外部配置（一般是与gitlab连用，既指定配置文件所在的gitlab地址） 
   springcloudconfig似乎不支持某些格式的ssh key访问git.(SpringCloudConfig访问git的组件不支持openssh这种格式的秘钥。使用git bash可以ssh访问，但是springconfig无法访问，建议使用http方式)
   本身也是一个微服务，分为server端和client端，server端负责连接git,客户端需要将配置写在bootstrap.yml里（客户端读取的属性值不会自动刷新，需要加点小配置并且发送一个post请求才会刷新）
   #### bus总线
   与spring-cloud-config配合使用，实现配置的动态刷新，需要绑定rabbitmq或activemq（之前需要往每个客户端发送post请求，现在只需要向config服务端自己发送一次post即可）
   ### 消息驱动
   #### cloud-stream
   屏蔽底层消息中间件的差异，统一消息模型（类似于orm框架），目前仅支持rabbitmq和kafka
   input消费者，output生产者
   stream中同一个组的服务消息只有一个接收，不同组的会广播通知,建议设置group
   ### 链路跟踪
   #### sleuth
   与zipkin配合使用  https://www.cnblogs.com/roadlandscape/p/12934407.html
   下载zipkin jar包并启动zipkin(相当于一个监控服务)
   将需要跟踪的链路注册到监控服务上
## springcloud alibaba
   ### nacos
   #### 简介
   服务注册与配置中心(naming config service)   eureka + config + bus
   #### 服务注册
   默认端口8848
   由于nacos继承了ribbon，所以自带负载均衡
   nacos支持cp与ap切换，发送一条post请求

   #### 配置中心
   配置文件位置由之前的git改为了nacos上
   bootstrap.yml用来存放nacos的地址信息
   application.yml用来指定要使用的文件名
   nacos上的文件名格式 ${spring.application.name}-${appliction中配置的文件名}.${bootstrat中配置的文件后缀} 
   实时刷新
   由dataID,groupId,namespace三部分组成： namespace是可以用于区分部署环境的，Group和DataID逻辑上区分两个目标对象
   #### 持久化
   nacos一些数据，例如配置文件等，需要进行持久化。单机会存于一个nacos内嵌的数据库derby中，但是使用集群时要使用一个统一的mysql存储
   

   ### sentinel
   #### 简介
   类似于hystrix的一个工具，使用jar包启动，需要监控的模块注册到jar包对应端口，还需要一个端口进行心跳检测
   使用的懒加载，api需要被调用后才会显示在sentinal上

   #### 流控规则
   控制某个api的QPS等
   ##### 类型
   QPS: 每秒的请求个数
   线程数: 保证当前时刻该api对应的线程数不高于某个值
   ##### 模式
   直接： 当不满足条件时，直接拒绝该ap的请求
   关联：在A上关联B API，当B的访问量超过设置的阈值时，拒绝A
   ##### 效果
   直接失败： 返回 Blocked by Sentinel (flow limiting)
   预热： 使qps慢慢增加。 会要求设置一个预热时长，初始的qps为 设置的最大阈值/3,然后再预热时长后达到最大阈值
   排队等待： 到达最高阈值时，不是直接拒绝请求，而是使请求排队，当超过所设置的超时时间再拒绝

   #### 降级
   sentinel里的降级就是熔断
   ##### 降级策略
   RT: 秒级反应时间，两个参数RT与时间窗口.  RT为该api最大响应时间，当一秒内有5个请求超过这个时间，该api会在时间窗口时间内熔断
   异常比例： 当一秒内有5个请求超过这个时间且当每秒异常的请求（只将抛出异常视为异常请求）数达到某个比例时，该api在时间窗口内熔断
   异常数： 一分钟内的异常数量打到某个数值时，熔断该api
   
   #### 热点规则
   可以配置针对api的某个参数的熔断规则(比如说需要传入用户id,那么针对id这个参数配置规则,这样可以限制一定时间内某个用户的访问次数)
   在需要热点配置的方法上要添加 @SentinelResource 才可以生效(资源名称需要与注解的value值相等)
   高级设置中，可以把某些特殊值排除在外，既特殊值可以不限流

   #### 系统规则
   针对整个系统制定规则(比如系统qps达到某个阈值,cpu达到某个利用率等),不是很推荐使用

   #### @sentinelResource
   配置自定义的流控/熔断页面
   blockHandler = "xxxMethod" 用于处理违反配置的api  ,  fallback = "xxxMethod" 用于处理runtimeException(如果方法只配了fallback，BlockException也会被接收), exceptionToIgnore 使某些异常不走fallback方法
   也可以配置全局的方法，注意该方法需要设置为static, blockHandlerClass=xxx.class blockHandler= "xxxMethod"
   注意： 自定义方法需要与controller的方法保持相同的参数,并且最后加上BlockException xxx

   #### 持久化
   配置的规则默认是临时的，重启sntinel或者重启项目就会消失
   将配置规则写在nacos中，把需要规则监控的模块与Nacos中的配置文件绑定
   https://blog.csdn.net/qq_40777074/article/details/106860713

   ### seata
   用来解决分布式事务问题的服务
   https://blog.csdn.net/qq_41910252/article/details/122517092
   TC： seata服务器    TM：需要注解的方法   RM：连接的数据库

## 大数据
   大规模的数据进行存储，分析，计算. TB,PB,EB级别
   ### hadoop
   #### 简介
   分布式大数据计算与存储的框架，由google的两篇论文所衍生出来
   #### 组成
   hdfs,mapredurce,yarn
   #### hdfs
   分布式文件系统，用于存储数据，将一个文件分成多个块(一个块一般是128m，如果文件不足128m会把该块共享给其他文件。设置128m是因为hdfs建议一秒内完成块传输，而机械硬盘一般是100MB/s)，存到集群中。 
   存储后的文件不能修改内容，只能追加内容，不适合保存小文件(namenode中会记录文件位置，本身也要占用空间)
   NameNode：用来记录数据存储在哪些机器上
   SecondryNameNode：NameNode的备份节点
   DataNode：具体存储据的机器
   自带一个web页面，可以查看存储的文件
   客户端上传文件时，会把文件进行拆分，分成一个个块。

   #### mapreduce
   用于将大任务分成多个小任务(map),再将结果合并(reduce)
   #### yarn
   负责调度mapreduce
   ResourceManager: 整个集群的资源(内存和cpu)调度节点
   NodeManager: 管理某台机器的资源(会把某台机器的资源分成很多container)

## 微服务
   ### 简介
   将一个大的服务拆分成为多个小的服务 <br />  
## 设计模式
   ###
## 编码规范
   ### java代码
   #### 属性命名
   变量的命名一律采用驼峰式，不要在乎变量名的长度，表达完整意思即可<br />
   常量名一律大写加下划线分割<br />
   包名全部小写，用点来分割单词<br />
   类名如果使用设计模式要写上设计模式名称，枚举后面跟上enum<br />
   对于boolean类型的变量，不要以isxxx命名（boolean的默认get方法也是isxxx,可能会出现问题）<br />
   ### 代码格式
   运算符或关键字左右用空格，小括号内不加<br />
   弃用tab,改为4个空格<br />
   注释与//间留一个空格就好<br />
   链式调用每个·换个行<br />
   空行一次加一个即可，没必要多加<br />
   ### 书写规范
   浮点数比较不要用 == 或者equals,可能出现不准的情况，可以采用比较差值<br />
   实体类的基本类型要写成封装类(避免空指针)<br />
   实体类一定要写toString方法<br />
   遍历map是要使用entryset，而不是keyset<br />
   switch判断字符串时，要进行非空判断<br />
   使用正则时，要将pattern设置static<br />
   对于 调用频率低，耗时比较长，需要极其稳定或者比较公开的接口，都要去进行参数校验。 校验一般放在controller层<br />
   ### java书写的一些小技巧
   使用 Objects.equals 方法替换entity.equals方法（可以避免空指针）<br />
   操作集合时多考虑使用stream流<br />
   for循环拼接string使用stringbuilder代替<br />
   创建集合是应该思考一下大概的长度<br />
   字符串比较时最好加一个全转小写<br />
   retry逻辑可以尝试用@RetryOnFailure来实现(依赖问题有点难解决)
  ### mysql相关
   #### 建表的规范
   表达是与否类型的字段，使用is_xxx命名，类型为unsigned tinyint(mysql中其实没有boolean,boolean就是tinyint(1))<br />
   表名全部小写<br />
   要注意避免出现保留字： range,match,case等<br />
   索引名称要符合规范： 主键pk_  唯一键uk_ 普通索引idx_<br />
   小数类型使用decimal,而不是float/double(可能缺失精度)<br />
   表一定要有的三个列： id,create_time,update_time<br />
   不要使用外键，在应用层处理<br />
   #### 索引相关
   只要该表的某个字段（或某些字段）具有唯一性，就应该建一个唯一索引。
   多表查询时，要尽量保证关联的字段有索引。
   #### 查询相关
   分页时利用子查询来优化查找
   使用count(*)而不是count(列名)，第二种会导致忽略掉null值的列
   尽量避免select * ,而是要指定返回的列
