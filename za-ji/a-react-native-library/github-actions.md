# Github Actions

`GITHUB_TOKEN`

`secrets.GITHUB_TOKEN` 是 GitHub Actions 提供的一个内置的、自动创建的 secret，用于在工作流程中进行身份验证。GitHub Actions 在每次工作流程运行时都会为你的仓库创建一个仅用于该运行的特殊访问令牌。

这个特殊的访问令牌具有适当的权限，使其可以执行工作流程中的常见操作，例如推送代码、创建分支、发出问题评论等。通常，`secrets.GITHUB_TOKEN` 是在执行 GitHub Actions 工作流程期间使用的默认身份验证令牌。

在 GitHub Actions 的工作流程中，你可以像使用其他 secrets 一样引用 `secrets.GITHUB_TOKEN`，例如：

```yaml
name: Example Workflow

on:
  push:
    branches:
      - main

jobs:
  example-job:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Use GitHub Token in the workflow
      run: echo ${{ secrets.GITHUB_TOKEN }}
```

这个内置的 `GITHUB_TOKEN` 允许你在工作流程中进行与仓库相关的操作，而无需手动创建其他 secrets。请注意，它在每个工作流程运行期间都会被自动创建和使用，而且不需要手动管理它的值。
