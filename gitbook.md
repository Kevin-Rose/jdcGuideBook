```
$ npm install gitbook-cli -g
```

GitBook 是一个基于 Node.js 的命令行工具，下载安装 Node.js，安装完成之后，你可以使用下面的命令来检验是否安装成功。

$ node -v
v7.7.1
安装 GitBook
输入下面的命令来安装 GitBook。

$ npm install gitbook-cli -g
安装完成之后，你可以使用下面的命令来检验是否安装成功。

$ gitbook -V
CLI version: 2.3.2
GitBook version: 3.2.3
更多详情请参照 GitBook 安装文档 来安装 GitBook。

编辑器
可以用 VsCode、Typora 等自己喜欢的来编辑。

先睹为快
GitBook 准备工作做好之后，我们进入一个你要写书的目录，输入如下命令。

```
$ gitbook init
```

warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
可以看到他会创建 README.md 和 SUMMARY.md 这两个文件，README.md 应该不陌生，就是说明文档，而 SUMMARY.md 其实就是书的章节目录，其默认内容如下所示：

# how to handle error 

* [Introduction](README.md)
接下来，我们输入 $ gitbook serve 命令，然后在浏览器地址栏中输入 http://localhost:4000 便可预览书籍。


#安装问题
我们打开/opt/node-v12.19.0-linux-x64/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js

在该文件的62~64行找到如下的代码：

fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)