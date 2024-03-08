# 💻 记录一次Mac前端环境配置

{% hint style="info" %}
全程未采用代理仓库来配置，配置代理仓库繁琐，且容易出问题。
{% endhint %}

* 配置基本`mac`开发环境

{% code overflow="wrap" lineNumbers="true" %}
```shell
xcode-select --install
# or download Xcode
```
{% endcode %}

* 安装[`oh-my-zsh`](https://ohmyz.sh/#install) `// 推荐安装`&#x20;
* 安装包管理工具[`homebrew`](https://brew.sh/)
* 安装`nvm`

<pre class="language-shell" data-overflow="wrap" data-line-numbers><code class="lang-shell"><strong>brew install nvm
</strong></code></pre>

* 安装`mysql/nginx/redis .etc`
* 安装`watchman`

<pre class="language-shell"><code class="lang-shell"><strong>brew install watchman
</strong></code></pre>

* 安装`cocoapods`

```sh
brew install cocoapods
```

* `Android`开发环境配置需要安装`jdk`

```sh
brew tap homebrew/cask-versions
brew install --cask zulu17

# Get path to where cask was installed to double-click installer
brew info --cask zulu17
```

android 环境变量配置

