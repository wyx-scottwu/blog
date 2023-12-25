# reset

`git reset` 是 Git 中的一个命令，用于移动 HEAD 指针和分支引用，从而改变工作目录的状态。它有不同的用法，主要有三个模式：`soft`、`mixed`、`hard`。

#### 1. Soft Reset:

Soft reset 仅仅移动 HEAD 指针，不改变索引区和工作目录。

```bash
git reset --soft <commit-hash>
```

这样会<mark style="background-color:red;">撤销某次提交</mark>，并将这次提交的更改保留在工作目录和索引中，你可以对这些更改进行修改后重新提交。

#### 2. Mixed Reset:

Mixed reset 是 **默认** 的 reset 模式，它会移动 HEAD 指针和更新索引区，但不会修改工作目录。这意味着工作目录中的更改仍然存在，但<mark style="background-color:red;">被标记为未提交的更改</mark>。

```bash
git reset --mixed <commit-hash>
```

#### 3. Hard Reset:

Hard reset 移动 HEAD 指针、更新索引区，并且强制性地将工作目录恢复到指定提交的状态。这<mark style="background-color:red;">将删除未提交的更改</mark>，请小心使用。

```bash
git reset --hard <commit-hash>
```

这样会丢弃所有在 `<commit-hash>` 之后的提交，并使你的工作目录变成与指定提交相同的状态。

#### 使用 HEAD 和 相对引用:

你也可以使用相对引用，比如 `HEAD~n`，表示相对于当前 HEAD 的第 n 个父提交。例如：

```bash
git reset --soft HEAD~1
```

这将撤销最后一次提交，并保留更改在工作目录和索引中。

请注意，在使用 `git reset` 时要小心，特别是在已经共享的分支上。如果你修改了历史记录并推送到远程仓库，可能会导致其他人的问题。
