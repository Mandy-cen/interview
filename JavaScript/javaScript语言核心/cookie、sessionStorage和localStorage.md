# cookie、sessionStorage和localStorage

## 目录
- [cookie](#cookie)
- [sessionStorage](#sessionStorage)
- [localStorage](#localStorage)
- [cookie、sessionStorage和localStorage的区别](#区别)

### <a id="cookie">cookie</a>
#### 1. 存储上限：4kb。
#### 2. 特点：每次http传输都会被自动带上，在secure字段设置为true的时候，只有当前地址才能读取。server端设置http-only，那么js就无法操作cookie了。
#### 3. 有效期：默认tab页关闭后就失效了，可以通过expire设置。
#### 4. 作用域：由domain和path确定。具体规则是domain是当前域名或者当前域名的父域名，当前path或者当前path的父path
#### 5. 存储的地方：虽然我们能在请求头中拿到cookie，其本质应该还是存在硬盘中的。
#### 6. 应用场景：每次信息处理都需要和server端交互的情景。
#### 7. 缺点：存储量少，操作麻烦，增加传输负担。

#### 设置／修改 cookie
cookie的原生的API，需要我们自己进行封装

```javascript
// 原生方式
const now = new Date();  
now.setTime(now.getTime() +1 * 24 * 60 * 60 * 1000);//转毫秒 
document.cookie = `name=Apple;expires=${now.toUTCString()};`

//封装setCookie方法
//setCookie 首先对name和value进行编码
function setCookie(name,value,expires,path,domain,secure){
    let cookie = encodeURIComponent(name)+ '=' +encodeURIComponent(value);
    //注意分号后面要有空格
    //后面的4个参数是可选的，所以用if判断并追加
    if(expires){
        cookie +='; expires='+expires.toGMTString()
    }
    if(path){
        cookie += '; path='+path
    }
    if(domain){
        cookie += '; domain='+domain
    }
    if(secure){
        cookie += '; secure='+secure
    }
    document.cookie = cookie;
}
```
#### 获取cookie
```javascript
function getCookie (name) {
    const arr = document.cookie.match(new RegExp('(^| )' + name + '=([^;]*)(;|$)'))
    return !arr ? unescape(arr[2]) : null
  }
``` 

#### 删除cookie
输入参数为name、path、domain 这3个是唯一标识cookie的,将max-age设置为0，就可以立即删除了。也可以利用设置过期时间达到删除效果。
```javascript
function remove(name,domain,path){
    document.cookie = `name=${name};domain=${domain};path=${path};max-age=0`
    // 设置过期时间
    document.cookie = `name=${name};expire=0`
}
```

### <a id="sessionStorage">sessionStorage</a>
#### 1. 存储上限：5~10mb左右，不同厂商略有差异。
#### 2. 特点：关闭tab页就没了，没有做持久化， 同步操作。
#### 3. 有效期：关闭tab页就没了。
#### 4. 作用域：同源（同端口，同域名，同协议）。
#### 5. 存储的地方：应该是内存中，但是存取速度还是非常的慢，测量了一次存1mb的数据需要半小时）。
#### 6. 应用场景：不需要做持久化，少量数据处理不用每次都和后端交互的情况。
#### 7. 缺点：存储量较少，性能随着容量减小显著下降，不同项目都存在一起，维护困难，只能保存字符串。

#### 设置&读取
```javascript
// 设置
window.sessionStorage.name= 'Sam'
//注意，如果要储存的数据对象、数组
//那么在储存之前，用JSON.stringify将数据转换为字符串
//读取之后，再用JSON.parse转换为对象、数组
window.sessionStorage.obj = JSON.stringify({name:"Tom",age:18});
window.sessionStorage.arr = JSON.stringify([1,2,3,4]);

//读取
const name = window.sessionStorage.name
const obj = JSON.parse(window.sessionStorage.obj || {})
const arr = JSON.parse(window.sessionStorage.arr || [])
```

#### sessionStorage页面传值
```javascript
//有时会有这样的需求，我们从A页面获取的数据，需要在B页面发送给后端，这时就需要我们将数据从A页面传递到B页面。
//A页面
//首先检测Storage
if (typeof(Storage) !== "undefined") {
    sessionStorage.name=value
} else {
    sessionStorage.name = ''
}

//B页面
if (typeof(Storage) !== "undefined") {
    const B_name = sessionStorage.name;
}
```

### <a id="localStorage">localStorage</a>
#### 1. 存储上限：5~10mb左右，不同厂商略有差异。
#### 2. 特点：持久化, 同源文档不同tab页可以信息共享甚至监听修改，同步操作。
#### 3. 有效期：不删除就永久存在。
#### 4. 作用域：同源（同端口，同域名，同协议）。
#### 5. 存储的地方：硬盘。
#### 6. 应用场景：需要做持久化，少量数据处理不用每次都和后端交互的情况。
#### 7. 缺点：存储量较少，性能随着容量减小显著下降, 不同项目都存在一起，维护困难，只能保存字符串。

#### 设置localStorage
```javascript
 window.localStorage.setItem('localStorageName',JSON.stringify({name:"Tom",age:18}))
```

#### 获取localStorage里面的值
```javascript
const contactInfos=JSON.parse(localStorage.getItem(localStorageName))
```

#### localStorage应用场景
localStorage可以用于存储该浏览器对该页面的访问次数，当然，如果换个浏览器，这个次数就重新开始计数了。还可以用来存储一些固定不变的页面信息，这样就不需要每次都重新加载了，这个值也可以进行覆盖。
访问这个页面的时候，script 脚本会自动运行，localStorage.pagecount就会 ++ 了，从而达到统计页面访问次数的目的。
```html
<!DOCTYPE HTML>
<html>
<body>
<script type="text/javascript">
    if (localStorage.pagecount){
        localStorage.pagecount=Number(localStorage.pagecount) +1;
    } else {
        localStorage.pagecount=1;
    }
    document.write("Visits: " + localStorage.pagecount + " time(s).");
</script> 
    <p>刷新页面会看到计数器在增长。</p>
    <p>请关闭浏览器窗口，然后再试一次，计数器会继续计数。</p>
</body>
</html>
```

### <a id="区别">cookie、sessionStorage和localStorage的区别</a>
1. localStorage 长期存储数据，浏览器关闭数据也不会丢失
2. sessionStorage 数据在浏览器关闭后自动删除
3. cookie是网站为了标识用户身份存储在本地的，cookie始终在同源http请求中携带在浏览器和服务器之间来回传递，而localStorage和sessionStorage不会把数据发送给服务，仅在本地保存
4. cookie数据不会超过4k，localStorage和sessionStorage虽然大小也有限制，但是比cookie大得多，可以达到5M
5. localStorage存储数据永久，除非手动删除。sessionStorage数据在当前浏览器关闭后删除。cookie有过期时间设置，过期时间之前一直有效

