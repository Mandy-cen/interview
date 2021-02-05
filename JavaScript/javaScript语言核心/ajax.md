# Ajax
## 了解Ajax
* Asynchronous Javascript And Xml， Ajax技术核心是XMLHttpRequest对象（简称XHR），这是由微软首先引入的一个特性，其他浏览器提供商后来都提供了相同的实现

## Ajax起源
* ajax有点
    * 增加速度：减轻服务器的负担，按需加载数据，最大程度的减少冗余请求
    * 改善的用户体验：局部刷新页面，减少用户等待时间，带来更好的用户体验
    * 页面和数据分离：前后端分离，操作更灵活，后期维护更方便
    
## Ajax请求步骤

### 1.创建请求对象，返回一个异步请求对象
 `var xhr = new XMLHttpRequest()`

### 2.处理服务器返回数据
```javascript
xhr.onreadystatechange = function() {
  if (xhr.readyState == 4) {
    alert(xhr.responseText)
  }
}
```

### 3.设置请求参数，建立与服务器连接
`xhr.open('get', 'http://localhost/api/ajaxtext', true)`

### 4.向服务器发送请求
`xhr.send()`

## XMLHttpRequest对象属性方法
* open(type, url, async): 建立服务器的连接
    * type： 请求的类型get、post、delete...
    * url：数据请求的地址（API地址），一般由后端开发人员提供
        * 当页面访问地址，API两者一定要同域
        * 同域：协议，域名，端口三者一致（同源策略）
    * async：是否异步发送请求（true， false）， 默认为true
        * 同步： 按步骤顺序执行，前面代码执行完后，后面代码才会执行
        * 异步：与其它操作同时执行，也叫并发
    * send(data): 向服务器发送请求
        * data：可选参数，post请求时才生效，表示发请求时传送的数据字符串
`xhr.send('name=tom&age=10')`
            * 在某些浏览器中，如果不需要通过请求主体发送数据，则必须传入null
        * get请求的数据写在api地址后
`request.open('get', 'http://localhost/api/getData.php?start=1&limit=10')`
    * setRequestHeader(key,val):设置请求头
        * 设置请求头在open方法调用后设置
`xhr.setRequestHeader('content-type')`            

































