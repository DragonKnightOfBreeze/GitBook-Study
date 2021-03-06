# GitBook学习笔记

## 简略步骤

Github全局

```
在自己的仓库中，创建仓库：<username>.github.io，用于存储书籍文件
（<username>是github用户名）
```

Github

```
创建一个仓库<name>（<name>是仓库名）
建立一个名为gh-pages的分支（也可以直接使用master，需要在Settings页面中配置）
只要gh-pages中的内容符合一个静态站点要求，就可以在如下地址中进行访问：
https://<username>.github.io/<name>
```

控制台

```
# 定位到工作目录
cd ...
# 下载gitbook cli
npm install -g gitbook-cli
# 下载gitbook（用时较长）
gitbook -V
# 初始化gitbook
gitbook init
# 构建gitbook，生成html、js、css文件
gitbook build
# 部署gitbook（到本地）
gitbook serve
# 打开控制台中显示的部署网址，即可查看效果

# 定位到书籍目录，默认是_book
cd _book
# 初始化git仓库
git init
git add .
git commit -m "init"
git remote add origin <git_url>
git push -u origin master

# 导入word、html书籍
gitbook-convert <file_name>
```

注意

* gh-pages分支使用的是_book目录下的html文件，而非仓库目录下的md文件！
* 因此，一般需要两个仓库，一个仓库用于存储包括文档在内的项目文件，另一个仓库用于存储生成后的书籍文件。
* 也可以本地在_book目录下新建另外一个git仓库，让远程的gh-pages分支专门存储生成后的书籍文件。

测试链接

* [测试书籍项目地址](https://github.com/DragonKnightOfBreeze/test_gitbook)
* [测试书籍链接](https://dragonknightofbreeze.github.io/test_gitbook/)
* [测试书籍链接（中文）](https://dragonknightofbreeze.github.io/test_gitbook/zh-hans)
* [测试书籍链接（英文）](https://dragonknightofbreeze.github.io/test_gitbook/en)

## 解决方案

使用`gitbook-convert`转化文档为markdown文档

```
npm install -g gitbook-convert
gitbook convert [options] <file> [export-directory]
```

选项

| Short | Long             | Description                                                  | Type    | Default |
| ----- | ---------------- | ------------------------------------------------------------ | ------- | ------- |
| -t    | --document-title | Name used for the main document title                        | string  | null    |
| -a    | --assets-dir     | Name of the document's assets export directory               | string  | assets  |
| -m    | --max-depth      | Maximum title depth to use to split your original document into sub-chapters | integer | 2       |
| -p    | --prefix         | Prefix filenames by an incremental counter                   | flag    | false   |
| -d    | --debug          | Log stack trace when an error occurs                         | flag    | false   |

支持的格式

| Type                               | Extension |
| ---------------------------------- | --------- |
| Microsoft Office Open XML Document | .docx     |
| OpenOffice / Open Document Format  | .odt      |
| Docbook Markup Language            | .xml      |
| HyperText Markup Language          | .html     |

## 参考链接

[使用 Gitbook 打造你的电子书 - 知乎](https://zhuanlan.zhihu.com/p/34946169)

[Gitbook 输出 · Gitbook使用教程](http://caibaojian.com/gitbook/format/output.html)