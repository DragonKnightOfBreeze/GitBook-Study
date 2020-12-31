# docsify学习笔记

## 简略步骤

### 初始化

```
# 全局安装docsify-cli
npm install -g docsify-cli
# 初始化docs目录
docsify init docs
```

### 本地预览

```
# 本地部署docs目录
docsify serve docs
# 打开默认访问地址
# http://localhost:3000 
```

### 目录结构

* `README.md` 首页
* `Doc1.md` 文档1
* `Doc2.md` 文档2
* `zh-cn`
  * `README.md` 首页
  * `Doc1.md` 文档1
  * `Doc2.md` 文档2
* `en`
  * `README.md` 首页
  * `Doc1.md` 文档1
  * `Doc2.md` 文档2
* `index.html` 入口文件
* `.nojekyll` 用于阻止GitHub Pages忽略掉下划线开头的文件

## 解决方案

### 定制侧边栏

为了获得侧边栏，您需要创建自己的_sidebar.md，你也可以自定义加载的文件名。默认情况下侧边栏会通过 Markdown 文件自动生成，效果如当前的文档的侧边栏。

首先配置 `loadSidebar` 选项，具体配置规则见配置项#loadSidebar。

<!-- index.html -->

```
<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

接着创建 `_sidebar.md` 文件，内容如下

```
<!-- docs/_sidebar.md -->

* [首页](zh-cn/)
* [指南](zh-cn/guide)
```

需要在`./docs`目录创建`.nojekyll`命名的空文件，阻止GitHub Pages忽略命名是下划线开头的文件。

### 嵌套的侧边栏

你可能想要浏览到一个目录时，只显示这个目录自己的侧边栏，这可以通过在每个文件夹中添加一个 `_sidebar.md` 文件来实现。

`_sidebar.md` 的加载逻辑是从每层目录下获取文件，如果当前目录不存在该文件则回退到上一级目录。例如当前路径为 `/zh-cn/more-pages` 则从 `/zh-cn/_sidebar.md` 获取文件，如果不存在则从 `/_sidebar.md` 获取。

当然你也可以配置 `alias` 避免不必要的回退过程。

```html
<script>
  window.$docsify = {
    loadSidebar: true,
    alias: {
      '/.*/_sidebar.md': '/_sidebar.md'
    }
  }
</script>
```

你可以在一个子目录中创建一个 `README.md` 文件来作为路由的默认网页。

### 用侧边栏中选定的条目名称作为页面标题

一个页面的 `title` 标签是由侧边栏中选中条目的名称所生成的。为了更好的 SEO ，你可以在文件名后面指定页面标题。

```markdown
<!-- docs/_sidebar.md -->
* [Home](/)
* [Guide](guide.md "The greatest guide in the world")
```

### 显示目录

自定义侧边栏同时也可以开启目录功能。设置 `subMaxLevel` 配置项，具体介绍见 [配置项#sub-max-level](https://docsify.js.org/#/zh-cn/configuration?id=sub-max-level)。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

### 忽略副标题

当设置了 `subMaxLevel` 时，默认情况下每个标题都会自动添加到目录中。如果你想忽略特定的标题，可以给它添加 `<!-- {docsify-ignore} -->` 。

```markdown
# Getting Started

## Header <!-- {docsify-ignore} -->

该标题不会出现在侧边栏的目录中。
```

要忽略特定页面上的所有标题，你可以在页面的第一个标题上使用 `<!-- {docsify-ignore-all} -->` 。

```markdown
# Getting Started <!-- {docsify-ignore-all} -->

## Header

该标题不会出现在侧边栏的目录中。
```

在使用时， `<!-- {docsify-ignore} -->` 和 `<!-- {docsify-ignore-all} -->` 都不会在页面上呈现。

## 部署

### GitHub Pages

GitHub Pages 支持从三个地方读取文件

- `docs/` 目录
- master 分支
- gh-pages 分支

我们推荐直接将文档放在 `docs/` 目录下，在设置页面开启 **GitHub Pages** 功能并选择 `master branch /docs folder` 选项。

![github pages](https://docsify.js.org/_images/deploy-github-pages.png)

可以将文档放在根目录下，然后选择 **master 分支** 作为文档目录。你需要在部署位置下放一个 `.nojekyll` 文件（比如 `/docs` 目录或者 gh-pages 分支）

## 参考链接

[docsify](https://docsify.js.org/#/zh-cn/)

[基于Github Pages + docsify，我花了半天就搭建好了个人博客_Java成魔之路-CSDN博客](https://blog.csdn.net/m0_37965018/article/details/103841362)

[MPE插件文档的参考模版](https://github.com/shd101wyy/markdown-preview-enhanced/tree/master/docs)