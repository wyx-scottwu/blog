---
description: rebase 修改 commit date & auth date
---

# rebase 修改提交信息

要修改特定提交的日期，你可以使用 `git rebase` 命令结合 `-i` 选项来执行交互式 rebase，然后修改需要更改的提交。以下是具体步骤：

1. 首先，找到需要修改日期的提交的哈希值，你可以使用 `git log` 命令来查看提交历史，并找到你想要修改的提交的哈希值。

```bash
git log
```

2. 执行交互式 rebase，指定需要修改日期的提交的哈希值。假设你想修改的提交哈希值为 `<commit-hash>`。

```bash
git rebase -i <commit-hash>^
```

请注意，`^` 是为了包含指定的提交。这个命令将会打开一个文本编辑器，列出了所有从指定提交到当前 HEAD 之间的提交。

3. 在打开的文本编辑器中，你会看到一个类似于下面的界面：

```
pick abcdef1 Your commit message
pick 1234567 Another commit message
...
```

4. 在需要修改的提交行（`pick` 后面的行）前面改变命令，将其改为 `edit`：

```
edit abcdef1 Your commit message
pick 1234567 Another commit message
...
```

5. 保存并退出编辑器。
6. Git 会停在你指定的提交，现在你可以修改提交的日期了。执行以下命令：

```bash
GIT_COMMITTER_DATE="YYYY-MM-DD HH:MM:SS" git commit --amend --no-edit --date "YYYY-MM-DD HH:MM:SS"
```

确保将 `YYYY-MM-DD HH:MM:SS` 替换为你希望的日期和时间。

7. 然后继续 rebase 过程，使用以下命令：

```bash
git rebase --continue
```

8. 如果有更多的提交需要修改，重复步骤 6 和步骤 7。
9. 完成后，使用 `git log` 确认提交日期是否已被修改。
10. 如果修改日期的提交在远程仓库中已经存在，你可能需要使用 `git push --force` 强制推送来更新远程仓库中的历史记录。但请注意，强制推送可能会影响其他共享项目的成员，请谨慎使用。

记住，修改提交的日期会影响项目的历史记录，所以在执行这样的操作时要谨慎。
