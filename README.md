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
   ### eslint
   ### prettier
   ### this
   this有显示绑定，隐式绑定等概念，在react中使用时会涉及到bind等行为 https://www.cnblogs.com/DM428/p/7777539.html    
   怎么写bind比较优雅   https://blog.csdn.net/flytam/article/details/104760202  
## 网络安全
   ### ddos
   http://www.ruanyifeng.com/blog/2018/06/ddos.html
