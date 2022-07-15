# Git

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

## 常用命令

https://jrhar.blog.csdn.net/article/details/116703787

1. 克隆现有存储库  ：$ git clone 仓库地址

2. 创建一个新的本地存储库：$ git init

3. 配置git环境：git config --global

   用户名配置   git config --global user.name "你的用户名"

   邮箱配置       git config --global user.email "你的邮箱"

4. 创建本地空仓库：git init

5. 新建文件添加到本地仓库：git add、git commit -m

6. 改写提交：git commit --amend

7. 查看历史提交日志：git log

8. 回滚代码仓库：git reset --hard查看提交之后文件是否做了改动：git status

9. 修改缓存区内容：git add、git commit -m

10. 将改动文件添加到缓存区：git add

11. 将所有改动文件添加到缓存区：git add --all、git add .

12. 将文件撤销回到最近一次修改的状态：git checkout -- file

13. 查看单个文件可回滚版本：git log filename

14. 删除文件：git rm

15. 查看提交历史：git reflog

16. git基本组成框架：Workspace、Index / Stage、Repository、Remote

17. git rm后恢复文件：git rm、git reset、git checkout

18. git创建分支：git branch、git checkout

19. git切换分支：git checkout

20. git合并分支：git merge

21. git查看分支：git branch -a

22. git删除本地分支：git branch -D

23. git删除远程分支：git push origin --delete

24. 在开发中git分支的重要性

25. github将本地仓库关联到远程仓库：git remote add origin

26. git将远程仓库关联到本地和拉取指定分支、切换远程分支：git clone

27. github提交本地仓库到远程仓库：git add、git commit、git push

28. git修改分支名称：git branch

29. git保存当前工作切换分支：git stash

30. 将别的分支修改转移到自己的分支：git cherry-pick

31. git远程删除分支后本地git branch -a依然看得到的问题：git remote 

32. git强制合并分支：--allow-unrelated-histories

33. git拉取远程所有分支：git fetch

34. git子模块管理：git submodule

35. git分支开发步骤

36. git强制删除分支：git branch 

37. git查看不同分支的文件差异：git diff

38. git查看仓库信息：git remote

39. Git新增分支操作：git switch、git restore