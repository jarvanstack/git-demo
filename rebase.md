# git rebase -i

我们需要将多个 commit 整合为一个再推送到 GitHub

```bash
$ git log --oneline
404f8c3 doc(readme): 新增b3
ce64c6a doc(readme): 新增b2
1bbe07a doc(readme): 新增b1
d38622c doc(readme): 新增a1,a2,a3并删除v*
```

我们需要将

* doc(readme): 新增b3
* doc(readme): 新增b2
* doc(readme): 新增b1

3 个 commit 合并为 1 个并重新命名为 

* doc(readme): 新增b1,b2,b3 

(1) 

git rebase -i 

将需要合并的 commit 从 pick 修改为 s(将会向上合并到 doc(readme): 新增b1 这个commit)

```bash
pick 1bbe07a doc(readme): 新增b1
s ce64c6a doc(readme): 新增b2
s 404f8c3 doc(readme): 新增b3

# Rebase 346e749..404f8c3 onto 404f8c3 (4 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
```

:wq 保存

(2) 修改 commit 的信息

```bash
# This is the 1st commit message:

doc(readme): 新增b1

# This is the commit message #2:

doc(readme): 新增b2

# This is the commit message #3:

doc(readme): 新增b3

```

删除这些 commit 然后修改为

```
doc(readme): 新增b1,b2,b3 
```

修改完毕

```bash
$ git log --oneline
3fe77d9 (HEAD -> master) doc(readme): 新增b1,b2,b3
d38622c doc(readme): 新增a1,a2,a3并删除v*
```