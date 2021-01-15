## index.lock文件存在问题

```
  git add .
  
  提示：
      If no other git process is currently running, this probably means a
      git process crashed in this repository earlier. Make sure no other git
      process is running and remove the file manually to continue.
      
 解决办法：
      rm -f .git/index.lock
      
 结果：
      提示文件被占用，一直删除不成功
      
 发现：
     可能是git发生过崩溃，只要打开编辑器，index.lock文件就会出现，关闭编辑器，lock文件消失
     
 解决办法：
    关闭编辑器，lock文件消失
    打开git-bash工具
    git add .
    git commit -m "aaa"
    
    提交完成后，之后的现操作开始正常
    
 剖析：
    应该是同时使用git-bash和编辑器命令行时，编辑器命令行的终端crashed之后，只要打开编辑器就会出现lock文件
    所以我们就不让lock文件产生，使用一个git-bash终端编辑项目，等提交完成之后，保证只使用某一个客户端进行操作就好
```
