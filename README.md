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
   
   ### ThreadLocal
   https://www.jianshu.com/p/640f2c0ac4b0<br />  
   为什么value不作为弱引用   https://www.zhihu.com/question/399087116<br />  
   
   ### 序列化
   writeObject readObject来实现手动的存储与读取<br /> 
   transient声明的对象不主动序列化<br /> 
   
## 前端相关
   ### DOM与BOM
   BOM是浏览器对象模型，DOM是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作<br /> 
   每个浏览器提供操作dom bom的api<br /> 
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
   ### react
   将数据渲染成视图的工具<br /> 
   传统的操作dom会造成浏览器多次渲染，效率低<br /> 
   react采用组件化模式，声明式编码，以及虚拟dom,减少与真实dom的交互(可以实现dom复用等功能).虚拟dom的本质是个object<br />
   react生成li标签时，建议携带唯一的key<br />
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
   ### 静态页面，动态页面
   静态页面一般可以跟文件类似，通过url直接访问<br />
   静态资源：可以理解为前端的固定页面，这里面包含HTML、CSS、JS、图片等等，不需要查数据库也不需要程序处理，直接就能够显示的页面，如果想修改内容则必须修改页面，但是访问效率相当高。<br />
   动态资源：需要程序处理或者从数据库中读数据，能够根据不同的条件在页面显示不同的数据，内容更新不需要修改页面但是访问速度不及静态页面。<br />
   
   ### 跨域问题，cors
   只要协议，域名，端口号，有一个不一样，就会产生跨域问题<br />
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
   call()方法： 改变函数的所有者  https://www.w3school.com.cn/js/js_function_call.asp
   
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
