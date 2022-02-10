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
   ### commonjs,ES6,import和require
   commonjs和es6是两个关于模块化的标准  ：https://www.jianshu.com/p/58f49f69a2fb	<br /> 
   ES6标准发布后，module成为标准，标准使用是以export指令导出接口，以import引入模块。import和export时都是到node_module文件夹中<br /> 
   ### eslint
   是一个第三方插件，用来查看前端代码不规范的地方   使用方法：https://blog.csdn.net/guang_s/article/details/90231312
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
