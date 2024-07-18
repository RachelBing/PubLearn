分布式版本控制系统

From **廖雪峰**

Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。


集中式版本控制系统
	局域网合适的-CVS & **SVN**
	中央服务器

##### 分布式版本控制系统
	每个人都拥有完整的数据库
	上传修改内容
分支管理

PS D:\Code\Python> git init .
Reinitialized existing Git repository in D:/Code/Python/.git/
git add 保存更改
git commit 生成记录节点（快照）
git push
git pull
git clone

ls -h
显示隐藏


如果没把新建项目clone到本地后更改再上传，试图上传完全无关的项目：
![](Pasted%20image%2020240306223310.png)
添加项目对应的远端仓库，地址（参数2），名字叫learn_PY（参数1）
git remote add learn_PY https://github.com/RachelBing/Learn-PY

本地main分支上游为learn_PY远端仓库的main
git branch --set-upstream-to=learn_PY/main main
git branch main --set-upstream-to=learn_PY/main

从远端拉取
git pull --allow-unrelated-histories
先同步远端更改才能同步上去
git push 