# revert

`git revert` 是一个 Git 命令，用于撤销一个或多个提交。与 `git reset` 不同，`git revert` 不会修改历史记录，而是创建一个新的提交来撤销已有的提交。这是一种安全的方式，因为它不会修改已经被共享的提交历史。

以下是 `git revert` 的基本用法：

```bash
git revert <commit-hash>
```

这个命令将撤销指定提交（由 `<commit-hash>` 指定）引入的更改，并创建一个新的提交。如果你要一次性撤销多个提交，可以在命令中列出多个提交哈希值，或者指定一个提交范围。

例如，如果要撤销最后三个提交，可以执行：

```bash
git revert HEAD~3..HEAD
```

撤销提交时，Git 会打开一个文本编辑器，让你编辑撤销提交的提交消息。如果你想在命令行中提供提交消息，可以使用 `-m` 选项，例如：

```bash
git revert -m 1 <commit-hash>
```

其中 `-m 1` 表示使用主分支的父提交作为撤销提交的父提交。

`git revert` 还有其他一些选项，可以根据需要进行使用。你可以通过以下方式获取更多信息：

```bash
git help revert
```

或者查看 Git 文档中关于 `git revert` 的部分。
