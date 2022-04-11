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
   git revert是针对远端，通过提交一个新的commit,**撤销某几个commit**（新的commit的改动就是之前的反操作） <br />  

    
## Linux
   
   ### NFS与rpcbind
   https://www.cnblogs.com/me80/p/7464125.html<br /> 
   
   ### env与 bashrc,profile
   env的东西保存在bashrc和profile里面。<br /> 
   bashrc和profile在/etc和/home中都存在一份，/home中的相同内容会覆盖/etc中的。bashrc和profile本身也稍有区别<br /> 
   https://cloud.tencent.com/developer/article/1174426<br /> 
   
   ### 正则
   (.+)与(.+?)： (.+)默认是贪婪匹配 (.+?)为惰性匹配   https://www.cnblogs.com/ysk123/p/9896850.html<br /> 
   
   ### scp
   注意，使用scp时，如果最前面加了sudo，则当前登陆用户是root，可能没有对方机器的登陆权限<br /> 
   scp无法直接在target端执行sudo命令，所以只能把文件传输到target用户拥有write权限的目录下<br /> 
   
   ### bash语法
      #### sed
      用于对于多行文本的操作
   
## JAVA

   ### javaHome
   javahome配置在path中的顺序可能会影响配置效果<br />
   ### javac
   使用javac xx.java将一个java程序编译为xx.class文件，然后使用java xx执行 ！！(不要加.class)
   ### ClassPath
   在安装java时需要配置classpath,用于搜索.class文件位置。但是1.5以后已经不需要配了<br /> 
   ### 编译与解释
   解释执行：将编译好的字节码一行一行地翻译为**机器码** 执行。 <br /> 
   编译执行：以方法为单位，将字节码一次性翻译为**机器码** 后执行。<br /> 
   编译器看到的都是字节码文件！！！！！ <br /> 
   https://www.cnblogs.com/lingz/archive/2018/07/31/9394238.html<br /> 
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
   
   ### java http请求
   feign<br />
   ### stream流
   stream流使用时分为三步： 创建stream-----> 对steam操作 -----> 结束<br /> 
   其中每一步都有很多api   https://blog.csdn.net/y_k_y/article/details/84633001<br /> 
   关于flatmap:  使用情况是当map方法返回的是个集合时(如果返回的是一个集合，用Map得到的结果是类似于这样：list<Person[]> ， 而flatmap则是list<Person>)
   结束时可以对集合进行Collectors.groupby，返回一个map<br /> 
   还可以对两个stream流进行Stream.concat操作<br /> 
   stream流的操作是不改变原始数组的(foreach可以改变，但是要注意foreach时的stream流是否含有元素，如果之前进行了filter导致没有元素则不会改变任何东西)
   foreach与collect无法同时使用，filter作用于不同的结束符效果也不一样
   stream的并行：https://www.jb51.net/article/149901.htm<br /> 

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
    JVM使用TLAB来避免多线程冲突，在给对象分配内存时，每个线程使用自己的TLAB，这样可以避免线程同步，提高了对象分配的效率.<br /> 
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
   ### 与idea的坑
   idea版本需要与maven版本适应才能在idea中使用,并且新的项目总是使用idea自带的Maven
   ### 配置文件
   repository： 用来指明本地远程库（一个repository代表一个本地远程库）
   mirror: 用来指明下载远程仓库时的镜像
   plugin: maven的生命周期每个周期都是执行相应的插件，plguin可以不指定版本，会下载本地远程库的release版本
   ### dependencyManagement
   用于父pom，对于声明在父pom的该标签下的依赖，子工程可以不写版本号(子工程如果写了以子工程为准),并且父pom不会导入该包
   ### 包的管理
   每次导入的就是坐标文件夹下的Jar包.  
   对于import的类文件来说，是没有group与artifity的. 路径就是jar包中的路径.所以可能会存在不同Group或者artifity里面相同路径名称的类，这时候就只能根据在maven里面的依赖顺序决定使用的是哪个类文件
   ### 内部变量
   ${project.version} ： 用在子模块间互相引用时填写在version中
   ### 一些命令行参数
   nsu： maven的repository中可能有snapshot,默认会在使用时查看远端是否存在最新的，然后更新本地的，加上这个参数会停止这个过程(快照默认每次都会去看有没有最新的 https://blog.csdn.net/weixin_38608626/article/details/88011541)
   -T:  指定线程数
   
## mybatis
   ### retruntype map
   mybatis里当查询到的值用map接收时，key是列名,value是值
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
   ###  js语法相关
   call()方法： 改变函数的所有者(也可以理解为改变调用时的this)  https://www.w3school.com.cn/js/js_function_call.asp
   js中操作集合，使用foreach前，先想想有没有替代品（foreach能做的事比较多，没法直接看出来要干什么，而some,erery等函数则可以方便看清，并且代码量少）：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
   ### spa应用
   单页面应用，指只有一个页面。 点击页面中的链接不会刷新页面，而是局部刷新组件
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
   箭头函数的this是不变的，指向定义时的this. 普通函数的this是随着调用者改变的
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
    绑定事件时要写方法名，不要携带括号。携带括号意味调用函数，也就是把函数的值返回<br/>
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
   
   ### htpp请求
   #### time_wait
   在四次挥手中，客户端最后需要有一个time_wait的时间，以确保没有包存活。而这个time_wait对于高并发的时候则是很吃力的，所以对于高访问的机器可以适当调低，或者尝试使用长连接来减少连接数量<br/>
   netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'   查看数量<br/>
   #### keepalive_timeout
   传统的http请求都是在完成一次发送后结束连接，当指定了keepalive_timeout时，会在每次发送后开启计时，达到时间才关闭连接
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
## tomcat
   ### catalina.out
   catalina.out用来存储控制台打印的信息即标准输入的目的地,在log4j中配置的consoleappender也会输入到此. 一般都含有gc信息（jdk默认在gc时会向控制台输出信息，可以通过jvm potion关闭）
## postman
   ### basic auth
   basic auth实质就是在header里添加("authorization" , "Basic (name:password).toBase64")   
## restful
   ### 请求类型
   get: 查    post:新增   put:更新所有  patch:更新某个属性  delete:删除
   ### 规则
   url中只存在名词，不存在动词，并且最好与数据库的表名对应
## mysql
   ### 5.7安装
   分为免安装版和安装版，免安装版教程：https://www.cnblogs.com/itcui/p/15511683.html   网址：http://ftp.ntu.edu.tw/MySQL/Downloads/MySQL-5.7/   
   ### char比较时的坑
   对于值为null的char,任何判断都会为false. 例如 name != 'a',是不会包含name为null的数据的，需要在前面加上is null包含上null的数据
   ### 数据类型
    #### unsigned
    无符号类型
   ### 索引
    #### 索引失效
    https://www.cnblogs.com/wdss/p/11186411.html
   ### 语句优化
   使用group by 替换distinct
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
   
   #### @sentinelResource

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
