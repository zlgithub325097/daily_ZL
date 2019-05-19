Git学习网站

```
https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192
```

git 删除远程提交记录

```
# 1.通过找到想要退回到的commit_id
$ git log
# 2.本地回到上一个commit_id
$ git reset --hard <commit_id>
# 3.推送到服务器，一定要加 --force 参数
$ git push origin HEAD:master --force
```

git 版本回退

```

```

git 单个文件提交

git 文件修改对比

git 分支

git 提交日志

