### doctype(文档类型) 的作用是什么？
doctype是指浏览器使用哪种 HTML 或 XHTML规范，如果没有doctype文档就会出现混杂模式（怪异模式）
怪异模式：浏览器使用怪异模式解析页面，在怪异模式中页面是以比较宽松且向后兼容的模式展示
标准模式：浏览器以一种W3c标准解析渲染页面。在标准模式中浏览器以其支持的最高标准呈现页面。

### HTML 和 XHTML 有什么区别？
HTML超文本标记语言（hyper text markup language）
XHTML可扩展的超文本标记语言

### 如果网页内容需要支持多语言，你会怎么做？
```
HTML中的META标签:

　　<META HTTP-EQUIV=“Content-Type” CONTENT=“text/html; CHARSET=字符集">

　　不写，根据浏览器默认字符集显示

　　charset=gb2312 简体中文

　　charset=big5 繁体中文

　　charset=EUC_KR 韩语

　　charset=Shift_JIS 或 EUC_JP 日语

　　charset= KOI8-R / Windows-1251 俄语

　　charset=iso-8859-1 西欧语系(荷兰语,英语,法语,德语,意大利语,挪威语,葡萄牙语,瑞士语.等十八种语言)charset=iso-8859-2 中欧语系

　　charset=iso-8859-5 斯拉夫语系(保加利亚语,Byelorussian语,马其顿语,俄语,塞尔维亚语,乌克兰语等)

　　charset=uft-8 unicode多语言
```

### HTML5标签
常见的html5标签有：
>* `<section>` - 表单、清单、文章分块等内容
>* `<nav>` - 导航
>* `<article>` - 完整独立快内容
>* `<aside>` - 和页面内容关联度较低的内容
>* `<header>` - 网页的头部
>* `<footer>` - 文章底部
>* `<main>` - 主内容
>* `<figure>` - 文档有关图例
>* `<figcaption>` - 图例说明
>* `<mark>` - 被高亮文字
>* `<video>` - 视频
>* `<audio>` - 音频
>* `<source>` - 为 `video` 和 `audio` 指定媒体源
>* `<track>` - 为 `video` 和 `audio` 指定文本轨道（字幕）
>* `<canvas>` - 位图区域
>* `<svg>` - 矢量图
>* `<progress>` - 进度条
>* `<meter>` - 滑动条

作用：结构语义化
为什么需要语义化？
1.易修改、易维护
2.无障碍阅读支持
3.搜索引擎良好，利于SEO
4.面向未来的HTML,浏览器在未来可能提供更丰富的支持

### 替换元素和不可替换元素
替换元素 就是浏览器根据元素的标签和属性，来决定元素的具体显示内容
例如：
>* <img> 根据 src 属性来读取图片信息并显示出来
>* <input> 根据标签的 type 属性来决定是显示输入框，还是单选按钮。

替换元素有：`<img>`、`<input>`、`<textarea>`、`<select>`、`<object>`

不可替换元素：html大多数元素是不可替换的，及其内容直接展现给浏览器

### 行内元素

| 块级元素    | 行内元素 |
| --------   | -----  | 
| 独占一行，默认情况下宽度自动填充父元素宽度 | 宽度随元素内容变化，相邻的行内元素会排列在同一行内，直到一行排不下才会换行  |
| 可以设置 width,height | 设置width，height无效 |
| 可以设置margin和padding | 可以设置margin-left、margin-right、padding-left、padding-right |
| 对应display:block | 对应 display:inline |

常见的块级元素
>* `<div>` - 标签块
>* `<from>` - 表单
>* `<h1>`、`<h2>`、`<h3>`、`<h4>`、`<h5>`、`<h6>` - 标题1-标题6
>* `<hr>` - 水平线
>* `<ul>` - 无序列表
>* `<ol>` - 有序列表
>* `<li>` - 列表项
>* `<p>` - 段落
>* `<table>`、`<thead>`、`<tbody>`、`<td>`、`<tr>`、`<th>` - 表格元素

常见的行内元素
>* `<a>` - 超链接或者锚点
>* `<b>` - 字体加粗
>* `<br>` - 换行
>* `<code>` - 定义计算机代码文本
>* `<i>` - 斜体
>* `<img>` - 图片
>* `<input>` - 输入框
>* `<label>` - 为input进行标记/标注
>* `<button>` - 按钮
>* `<textarea>` - 多行文本

### HTML5新增属性

1.contentEditable规定是否可编辑元素的属性内容
`document.body.contentEditable=true;` 可以修改已发布网站

2.hidden: 隐藏元素。不会占用文档流

3. draggable: true为可拖动

4. data-* 自定义属性

例如:
js获得元素属性值：`obj.getAttribute("data-args")`
js设置属性：`obj.setAttribute("data-args", "123")`

通过目标节点获取
`e.target.dataArgs`、`e.currentTarget.dataArgs`

5. placeholder 占位属性

6. required 必填属性

7. pattern 正则属性

8. autofocus自动聚焦属性

9. autocomplete自动补全属性
当表单元素设置了自动完成功能后，会记录用户输入过的内容，双击表单元素会显示历史输入

10. novalidate不验证属性
属性规定在提交表单时不应该验证 form 或 input 域

11. multiple多选属性
属性规定输入域中可选择多个内容，如：email 和 file

12. contextmenu 指定右键菜单
