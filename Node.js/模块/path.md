# Node.js 模块：path

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Node.js 模块：path](#nodejs-模块path)
	- [方法](#方法)
		- [取文件名 path.basename (path, ext)](#取文件名-pathbasename-path-ext)
		- [取文件扩展名 path.extname(path)](#取文件扩展名-pathextnamepath)
		- [取路径目录名 path.dirname(path)](#取路径目录名-pathdirnamepath)
		- [解析路径为对象 path.parse(path)](#解析路径为对象-pathparsepath)
		- [路径对象格式化 path.format(pathObject)](#路径对象格式化-pathformatpathobject)
		- [是否为绝对路径  path.isAbsolute(path)](#是否为绝对路径-pathisabsolutepath)
	- [属性](#属性)
		- [系统分隔符 path.delimiter](#系统分隔符-pathdelimiter)

<!-- /TOC -->


文档：[Path - Node.js v6.2.0 Documentation](https://nodejs.org/api/path.html)

```javascript
var path = require("path");
```

## 方法




### 连接路径 path.join(path1, path2, ...)
用当前系统的路径分隔符来连接路径，返回结果。
```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..')
//  on *nix:		"/foo/bar/baz/asdf"
//  on Windows:	"\foo\bar\baz\asdf"
```


### 路径标准化 path.normalize(path)
把一个路径字符串标准化为当前系统的形式。会处理 `.` (此目录)、`..`（上一目录）。

```js

// Windows:
path.normalize('/foo/bar//baz/asdf/quux/')
// "\foo\bar\baz\asdf\quux\"

path.normalize("C:\\Program Files\\About.dll")
// "C:\Program Files\About.dll"

path.normalize("C:\\Program Files\\About.dll\\..")
// "C:\Program Files"

```

### 取文件名 path.basename (path, ext)

取路径中的文件名，ext 参数可以用来去掉文件名后的扩展名（注意要包括 `.`）。

```javascript
path.basename("C:\\Program Files\\About.dll")
//  'About.dll'

path.basename("C:\\Program Files\\About.dll", ".dll")
//  'About'
```

### 取文件扩展名 path.extname(path)
取路径中的文件扩展名（注意包括 `.`）。  
可以与 `path.basename()` 配合使用，取得没有扩展名的纯文件名：

```js
path.extname("E:\\学习\\前端\\JavaScript异步编程.pdf")
//  '.pdf'


var fileName = "E:\\学习\\前端\\JavaScript异步编程.pdf";
path.basename(fileName, path.extname(fileName));
//  'JavaScript异步编程'

```

### 取路径目录名 path.dirname(path)

```js
path.dirname('C:\\Program Files\\About.dll')
//   '"C:\Program Files"'
```


### 解析路径为对象 path.parse(path)
把路径解析为一个对象，其中是把路径分解的各个部分（根路径、路径目录名、文件名、扩展名、纯文件名）。  
使用 `path.parse(path)` 用来取路径的文件名、扩展名等部分是最方便的，比上面两个方法简洁。

``` js
path.parse('C:\\Program Files\\About.dll');
// Object
// {
//   root:  "C:\",
//   dir:   "C:\Program Files",
//   base:  "About.dll",
//   ext:   ".dll",
//   name:  "About"
// }

path.parse("E:\\学习\\前端\\JavaScript异步编程.pdf").name
//  "JavaScript异步编程"
```




### 路径对象格式化 path.format(pathObject)
把使用 `path.parse(path)` 生成的路径对象还原为路径字符串。

```js

path.format({
    dir:   "C:\\Program Files",
    base:  "About.dll"
});
//  '"C:\Program Files\About.dll"'

```

### 是否为绝对路径  path.isAbsolute(path)
判断一个路径是否为绝对路径。

```js
//  *nix:
path.isAbsolute('/foo/bar') // true
path.isAbsolute('/baz/..')  // true
path.isAbsolute('qux/')     // false
path.isAbsolute('.')        // false

//  Windows:
path.isAbsolute('//server')  // true
path.isAbsolute('C:/foo/..') // true
path.isAbsolute('bar\\baz')  // false
path.isAbsolute('.')         // false
```
### 取相对路径 path.relative(from, to)
`from`：源路径，  `to`：目的路径  
生成一个可以从“源路径”指向“目的路径”的相对路径。

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb')
// ..\\..\\impl\\bbb'

```
# 解析路径 path.resolve(from, from2, ..., to)
把给定的路径解析为绝对路径。
当有多个参数时会连续解析，相当于在命令行中连续输入 `cd` 命令。
不传入参数时会返回当前目录。

```js
// 当前运行文件目录："E:\Work\GitHub\limitPNG\"

path.resolve("./index.html")
// "E:\Work\GitHub\limitPNG\index.html"

path.resolve("./index.html", "..", "da", "bin")
// "E:\Work\GitHub\limitPNG\da\bin"

path.resolve()
// "E:\Work\GitHub\limitPNG\"

```


## 属性

### 路径分隔符 path.sep
当前系统中的路径分隔符，`/` 或 `\`。


### 路径分界符 path.delimiter
系统信息中多个路径间的分界符。
```js
//  *nix:
path.delimiter  //':'
//  Windows:    
path.delimiter  //';'

console.log(process.env.PATH)
// 'C:\Windows\system32;C:\Windows;C:\Program Files\node\'
process.env.PATH.split(path.delimiter)
//  ['C:\\Windows\\system32', 'C:\\Windows',
// 'C:\\Program Files\\node\\']
```

### \*nix 风格 path.posix
提供总以 \*nix 风格处理的 path 方法。

```js
path.posix.join("ddd","dsf")
// on Windows & *nix : "ddd/dsf"
```

### Windows 风格 path.win32
提供总以 Windows 风格处理的 path 方法。

```js
path.win32.join("ddd","dsf")
// on Windows & *nix : "ddd\dsf"
```
