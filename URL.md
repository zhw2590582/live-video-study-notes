### 参考
[https://developer.mozilla.org/zh-CN/docs/Web/API/URL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)

### 构造函数
URL()：使用给定参数创建并返回一个 URL 对象

### 实例属性
url.href：包含完整 URL 的 DOMString

url.protocol：包含 URL 协议名的 DOMString，末尾带 ':'

url.host：包含 URL 域名，':'，和端口号的 DOMString

url.hostname：包含 URL 域名的 DOMString

url.port：包含 URL 端口号的 DOMString

url.pathname：以 '/' 起头紧跟着 URL 文件路径的 DOMString

url.search：以 '?' 起头紧跟着 URL 请求参数的 DOMString

url.hash：以 '#' 起头紧跟着 URL 锚点标记的 DOMString

url.username：包含在域名前面指定的用户名的 DOMString

url.password：包含在域名前面指定的密码的 DOMString

url.origin：返回一个包含协议名、域名和端口号的 DOMString

url.searchParams：返回一个用来访问当前 URL GET 请求参数的 URLSearchParams 对象

### 实例方法
url.toString()：返回一个包含完整 URL 的 DOMString

### 静态方法
URL.createObjectURL()：静态方法会创建一个 DOMString，其中包含一个表示参数中给出的对象的URL。这个 URL 的生命周期和创建它的窗口中的 document 绑定。这个新的URL 对象表示指定的 File 对象或 Blob 对象

URL.revokeObjectURL()：静态方法用来释放一个之前通过调用 URL.createObjectURL() 创建的已经存在的 URL 对象。当你结束使用某个 URL 对象时，应该通过调用这个方法来让浏览器知道不再需要保持这个文件的引用了。