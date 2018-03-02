# HTML知识点整理

* [HTML相关文章收集](./articles.md)
* [HTML学习网站](./websites.md)
* [HTML书籍推荐](./books.md)

## 1、移动Web前端viewport解析

| name | value | description |
| ---- | ---- | ---- |
| width | 正整数或device-width | 定义视口的宽度 |
| initial-scale | [0.0 - 10.0] | 定义初始缩放值 |
| minimum-scale | [0.0 - 10.0] | 定义缩放最小比例，必须小于或等于maximum-scale设置 |
| maximum-scale | [0.0 - 10.0] | 定义最大缩放比例，必须大于或等于minimum-scale设置 |
| user-scalable | yes/no | 定义是否允许用户手动缩放页面 |

Basic usage：
``` html
  <meta name="viewport" content="width=deivce-width;initial-scale=1;minimum-scale=1;maximum-scale=1;" />
```

## 2、浏览器的标准模式（standards mode）和怪异模式（quirks mode）
标准模式下的浏览器支持的最高标准进行页面排版和渲染JS。  
兼容模式下的浏览器会模仿老浏览器的行为保证兼容性。

在HTML的头部要声明`DOCTYPE`，告诉浏览器以什么模式去渲染页面。如果没声明Doctype或者声明的格式错误，浏览器会以兼容模式去呈现页面。

Basic usage:
``` html
  <!doctype html>
  <html>
    <head></head>
    <body></body>
  </html>
  
```

## 3、link标签和@import标签的区别
1. link标签是XHTML标签，除了可以引用CSS，还可以引用图标和定义RSS等，@import只能用于引入样式。
2. link标签引入CSS时，在页面载入时样式同时加载。@import只是在页面加载完成之后才开始加载样式。
3. link标签是XHTML，无兼容性问题。@import是CSS2.1引入的，低版本浏览器不支持。