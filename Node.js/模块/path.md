文档：[Path - Node.js v6.2.0 Documentation](https://nodejs.org/api/path.html)

```javascript
var path = require("path");
```

## 取文件名 path.basename (path, ext)

取路径中的文件名，ext 参数可以用来去掉文件名后的扩展名（注意要包括 `.`）。

```javascript
path.basename("C:\\Program Files\\About.dll")
// returns 'About.dll'

path.basename("C:\\Program Files\\About.dll", ".dll")
// returns 'About'
```

## 取文件扩展名 path.extname(path)
取路径中的文件扩展名（注意包括 `.`）。
可以与 `path.basename()` 配合使用，取得没有扩展名的纯文件名：

```js
path.extname("E:\\学习\\前端\\JavaScript异步编程.pdf")
// returns '.pdf'


var fileName = "E:\\学习\\前端\\JavaScript异步编程.pdf";
path.basename(fileName, path.extname(fileName));
// returns 'JavaScript异步编程'

```

## 取路径目录名 path.dirname(path)

```js
path.dirname('C:\\Program Files\\About.dll')
// returns '"C:\Program Files"'
```


## 解析路径为路径对象 path.parse(path)
