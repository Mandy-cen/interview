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
`xhr.setRequestHeader('content-type'，'application/x-www-form-urlencoded')`
> 在请求服务器响应后，响应的数据会自动填充xhr对象的属性，相关的属性简介如下：
    
* readyState
    * 0 - 未初始化 尚未调用open()方法
    * 1 - 启动 已经调用open()方法但尚未调用send()方法
    * 2 - 发送 sand() 方法执行完成，但尚未接收到响应
    * 3 - 接收 已经接收到部分响应数据
    * 4 - 完成 响应内容解析完成，可以在客户端调用

> 只要readyState属性的值由一个值变成另一个值，都会触发一次readyStatechange事件。必须在open()之前指定onreadystatechange事件处理程序才能确保跨浏览器兼容性

* responseText - 保存服务器返回的数据（从服务器返回的数据是"字符串"）

* status - 响应的HTTP状态
    * 200（ok）- 服务器返回了页面
    * 304（not modified）- 数据与服务器相同，不需要从服务器重新请求（直接使用缓存的数据）
    * 400（bad request）- 语法错误导致服务器不识别
    * 401（unauthorized）- 请求需要用户认证
    * 404（not found）- 请求地址不存在
    * 500（internal Server Error）- 服务器出错或无响应
    * 503（service unavailable）- 由于服务器过载或维护导致无法完成请求
    
* statusText - HTTP状态码说明

## AJAX跨域解决方案

### JSONP
JSONP是JSON with padding（填充式JSON或参数式JSON）的简写
JSONP是一种可以绕过浏览器的安全限制，从不同的域请求数据的方法。使用JSONP需要服务器端提供必要的支持
`callback({"name": "ton"})`
> JSONP由两部分组成：回调函数和数据，回调函数是当响应到来时应该在页面中调用的函数

#### JSONP请求原理
* JSONP的原理是通过script标签发起一个get请求来取代xhr请求
    * JSONP生成一个script标签并插入到DOM中
    * 然后浏览器会接管并向src属性所指向的地址发送请求
    * 从服务器端返回一段js代码，这段代码就是一个函数的执行（执行时把数据作为参数传入，函数为本地预定义的函数），这个我们就间接的得到了服务器传出的数据
    
* 步骤如下
    * 1.预定义全局函数getData - 注意：必须为全局函数
    ```javascript
    function getData(data){
        console.log(data)
    }
    ```

    * 2.生成script标签，请求服务器地址，并附带函数名
    ```javascript
    <script src="http://localhost:8080/getJSONP?calback=getData"></script>
    ```

    * 3.服务器返回js文件（js文件里面包含我们预定义的函数执行），请求成功后，得到的js代码为
    ```javascript
    getData({name: 'Mandy', age: 18})
    ```

> JSONP 请求不是ajax请求，是利用script标签能加载其他域名的js文件的原理，来实现跨域数据的请求

* 缺点：这中方法只支持GET方式，不如POST方式安全

- demo
```javascript
function addScriptTag(src) {
  var script = document.createElement('script');
  script.setAttribute("type","text/javascript");
  script.src = src;
  document.body.appendChild(script);
}

window.onload = function () {
  addScriptTag('http://www.client.com?callback=getData');
}

function getData(data) {
  console.log('response data: ' + JSON.stringify(data));
};    
```


### CORS

CORS是一个W3C标准，全称是是-跨域资源共享（Cross-origin resource sharing）, 它允许浏览器向跨源服务器发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制
> CORS需要浏览器和服务器同属支持。目前，所有浏览器都支持改功能，IE浏览器不能低于IE10

* Access-Control-Allow-Origin
    * 该字段是必须的，需要在后段响应头添加该字段，值要么是一个* ，表示接受任意域名的请求，要么指定一个域名，如想指定若干个请使用判断语句
```javascript
// php
$allow_origin = array('http://www.client.com','http://www.client2.com')
if(in_array($origin, $allow_origin)){
    header('Access-Control-Allow-Origin:'.$origin);
} 
```

* Access-Control-Allow-Methods
* Access-Control-Allow-Headers
```javascript
header('Access-Control-Allow-Methods:POST');  
header('Access-Control-Allow-Headers:x-requested-with,content-type'); 
```

### 服务器代理
* 原理
Server Proxy，顾名思义，在服务器端设置一个代理，由服务器端向跨域的网站发出请求，再将请求结果返回给前端，成功避免同源策略的限制。

* 客户端请求

```javascript
$.ajax({
    url:'/proxy.php?name=camille&age=18',   //服务器端的代理程序
    type:'GET',
    success: function (data){

    }
})
```

* 在代理程序proxy.php中，向非同源下的服务器发出请求，获得请求结果，将结果返回给前端。

```
<?php 
    $name = $_GET['name'];
    $age = $_GET['age'];
    $crossUrl = 'http://b.com/sub?name='.$name;   //向其他域发出请求
    $res = file_get_contents($crossUrl);
    echo $res; 
 ?>
```












