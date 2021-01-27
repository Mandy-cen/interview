### cookie获取和写入
```javascript
// 设置cookie
var now = new Date();  
now.setTime(now.getTime() +1 * 24 * 60 * 60 * 1000);//转毫秒 
document.cookie = `name=Mandy;expires=${now.toUTCString()};`

// 获取cookie
const cookies = document.cookie
// 删除 利用设置过期时间达到删除效果
```

### cookie、sessionStorage和localStorage的区别
1. localStorage 长期存储数据，浏览器关闭数据也不会丢失
2. sessionStorage 数据在浏览器关闭后自动删除
3. cookie是网站为了标识用户身份存储在本地的，cookie始终在同源http请求中携带在浏览器和服务器之间来回传递，而localStorage和sessionStorage不会把数据发送给服务，仅在本地保存
4. cookie数据不会超过4k，localStorage和sessionStorage虽然大小也有限制，但是比cookie大得多，可以达到5M
5. localStorage存储数据永久，除非手动删除。sessionStorage数据在当前浏览器关闭后删除。cookie有过期时间设置，过期时间之前一直有效

