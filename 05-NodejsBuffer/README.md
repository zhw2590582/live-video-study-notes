## Nodejs 缓冲器

- [Node.js 中文网 buffer](http://nodejs.cn/api/buffer.html)
- [Github feross/buffer](https://github.com/feross/buffer)

现在的`nodejs`已经很好的支持`ES6`的`ArrayBuffer`，但`nodejs`有自己的一套处理二进制数据的接口叫`Buffer`，而且属性和方法还很多，其实只要仔细的看这些接口就发现用`TypedArray`也可以做到，而且`ArrayBuffer`和 `Buffer`可以互转，上面提到的 [Github feross/buffer](https://github.com/feross/buffer) 就是一个用`ArrayBuffer`实现的一个浏览器端的`Buffer`，看一下源码会加深对`Buffer`的理解，上面两个已经讲解得很清楚了，这里也不再累述。
