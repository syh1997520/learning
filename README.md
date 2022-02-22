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
#### git reset 与 git rever  
   git reset是用于本地的branch(未push的), **将暂存区的commit回到某个commit的时候**，工作区不动<br />
   git revert是针对远端，通过提交一个新的commit,**撤销某几个commit**（新的commit的改动就是之前的反操作） <br />  

    
## Linux
   
   ### NFS与rpcbind
   https://www.cnblogs.com/me80/p/7464125.html
   
   ### env与 bashrc,profile
   env的东西保存在bashrc和profile里面。
   bashrc和profile在/etc和/home中都存在一份，/home中的相同内容会覆盖/etc中的。bashrc和profile本身也稍有区别
   https://cloud.tencent.com/developer/article/1174426
   
   ### 正则
   (.+)与(.+?)： (.+)默认是贪婪匹配 (.+?)为惰性匹配   https://www.cnblogs.com/ysk123/p/9896850.html
   
   
## JAVA
   ### ClassPath
   在安装java时需要配置classpath,用于搜索.class文件位置。但是1.5以后已经不需要配了<br />  
   
   ### ThreadLocal
   https://www.jianshu.com/p/640f2c0ac4b0<br />  
   为什么value不作为弱引用   https://www.zhihu.com/question/399087116<br />  
   
   ### java http请求
   feign<br />

   ### IO操作
   - inputWriter<br />
   创建inputWriter对象时，需要传一个boolean参数，用来控制是否为追加输入(默认false)<br />
   
   ### 序列化
   writeObject readObject来实现手动的存储与读取<br /> 
   transient声明的对象不主动序列化<br />
   ### JVM

   
## 前端相关
   ### mdn
   web开发手册，包含js的使用规则等等
   ### DOM与BOM
   BOM是浏览器对象模型，DOM是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作<br /> 
   每个浏览器提供操作dom bom的api<br /> 
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
    新版本中与will相关的生命周期都不推荐使用了  
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
     通过react-router插件实现
  - UI框架
     antd  蚂蚁出品
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
   url中，localhost:8080/usr?name=10  这种查询，叫做query式url   localhost:8080/usrname=10   这种叫做param式<br />
   express中的路由是模块化的。既一个路由是由多个js文件注册在一起的。<br />
   express中有一个中间件的概念： 一个req,res可以由多个函数处理，这里的处理函数就叫做中间件<br />

    ### nodemon
    一个热重启的插件，使用nodemon xx.js  启动js文件，可以在保存后自动重启项目<br />

   ###  js语法相关
   call()方法： 改变函数的所有者(也可以理解为改变调用时的this)  https://www.w3school.com.cn/js/js_function_call.asp
   
   ### eslint
   是一个第三方插件，用来查看前端代码不规范的地方   使用方法：https://blog.csdn.net/guang_s/article/details/90231312<br />
   ### prettier
   ### this
   this有显示绑定，隐式绑定等概念，在react中使用时会涉及到bind等行为 https://www.cnblogs.com/DM428/p/7777539.html    
   怎么写bind比较优雅   https://blog.csdn.net/flytam/article/details/104760202  
   ### package.json与package-lock.json
   package.json类似于pom文件，package-lock是用来锁定版本号的
   在npm install时，如果lock与packgae版本兼容，则依据lock.不兼容则更新lock
## 网络安全
   ### ddos
   http://www.ruanyifeng.com/blog/2018/06/ddos.html
## Redis
   ### 默认配置
   redis默认的内存是0，既无上限。默认清除策略是不清除。所以要设置过期时间
   过期时间的最小单位是key,对于map,list等结构，一次清除，全部清除（redisson中具有实现value过期的map）
   ### redission使用手册
   https://www.bookstack.cn/read/redisson-wiki-zh
  
