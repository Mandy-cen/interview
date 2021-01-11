### CSS 3 新特性
1.过渡transition
```
// 分开写
transition-property: width;
transition-duration: 1s;
transition-timing-function: linear;
transition-delay: 2s;
```
2.animation

3.transform
transform:适用于2D或3D旋转
属性：
（1）rotate, rotateX, rotateY, rotate3D
（2）translate
（3）scale
（4）skew

4.阴影
语法：`box-shadow: 水平阴影的位置 垂直阴影的位置 模糊距离 阴影的大小 阴影的颜色 阴影开始方向（默认是从里往外，设置inset就是从外往里）;`

5.边框
(1) border-image
语法：`border-image: 图片url 图像边界向内偏移 图像边界的宽度(默认为边框的宽度) 用于指定在边框外部绘制偏移的量（默认0） 铺满方式--重复（repeat）、拉伸（stretch）或铺满（round）（默认：拉伸（stretch）`
(2) border-radius


6.背景
background-clip
background-origin
background-size

7.倒影
语法：`-webkit-box-reflect:方向[ above-上 | below-下 | right-右 | left-左 ]，偏移量，遮罩图片`

8.文字
语法：`word-break: normal|break-all|keep-all;`
语法：`word-wrap: normal|break-word;`

超出省略：
```css
div {
    width: 200px;
    border: 1px solid #ccc;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
```

多行超出省略：
```css
div {
    width: 300px;
    overflow: hidden;
    border: 1px solid #ccc;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
}
```

文字阴影： `text-shadow`

9.颜色:rgba,hsla
10.渐变
11.滤镜
12.弹性布局 flex
13.栅格布局 grid
14.盒模型 box-sizing
15.媒体查询
媒体查询，就在监听屏幕尺寸的变化，在不同尺寸的时候显示不同的样式！在做响应式的网站里面，是必不可少的一环！不过由于我最近的项目都是使用rem布局。所以媒体查询就没怎么用了！但是，媒体查询，还是很值得一看的！说不定哪一天就需要用上了！
```css
body {
    background-color: pink;
}
@media screen and (max-width: 960px) {
    body {
        background-color: darkgoldenrod;
    }
}
@media screen and (max-width: 480px) {
    body {
        background-color: lightgreen;
    }
}
```
