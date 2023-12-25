# 🔀 Git

#### git reset & git revert

`git reset` 和 `git revert` 有一明显区别：

`git revert` 指哪打哪，即 `git revert <commit-hash>`  `commit-hash` 即为`revert`目标

而 `git reset <commit-hash>` 要操作的`commit-hash` 需要为目标`hash`上一个即更早`commit`的那个`commit-hash`
