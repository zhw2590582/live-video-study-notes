## 类型数组

类型数组二进制数据的一个接口，有了它就不像用位运算符操作数据那么痛苦，以下两个链接都把类型数组讲得很清楚，以后会大量用到这个接口，可以当手册查看。

- [ECMAScript 6 入门 - ArrayBuffer](http://es6.ruanyifeng.com/#docs/arraybuffer)
- [MDN web docs - ArrayBuffer](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

## ArrayBuffer

首先是`ArrayBuffer`只负责声明二进制数据，比较简单

```js
// 通过字节大小声明ArrayBuffer
const buf = new ArrayBuffer(32);

// 返回是否视图
ArrayBuffer.isView;

// 返回字节大小
ArrayBuffer.prototype.byteLength;

// 拷贝新的 ArrayBuffer
ArrayBuffer.prototype.slice;
```

## TypedArray

然后是`TypedArray`，有 `9` 种类型，其中`Uint8Array`是最常见的，因为一个元素就表示一个字节，而且无符号没有负数没有小数的情况，更直观方便。`TypedArray`声明方式有很多，原型对象上有很多类似`Array`的原型的方法，但有几个特殊的属性和方法。

为什么有这么多种构造函数？因为单种如`Uint8Array`表示的数值是有限的。

例如在`Uint8Array`里，一个元素代表一个字节，一个字节最大表示数位为`255`，但很多时候`255`满足不了，那就用两个字节表示那就是最大数值可以达到`255 * 255`也就是`0b1111111111111111`或者`0xffff`为`65535`，那么这就适合使用两个字节为一个元素的`Uint16Array`了，或者四个字节为一个元素的`Uint32Array`。

```js
// 每个元素的字节大小，这里就是一个字节
TypedArray.prototype.BYTES_PER_ELEMENT;

// 占据的内存长度，单位为字节
TypedArray.prototype.byteLength;

// 从底层ArrayBuffer对象的哪个字节开始
TypedArray.prototype.byteOffset;

// TypedArray 数组含有多少个成员
TypedArray.prototype.length;

// 用于复制数组
TypedArray.prototype.set;

// 对于 TypedArray 数组的一部分，再建立一个新的视图，但还是属于同一段数据
TypedArray.prototype.subarray;

// 返回一个指定位置的新的TypedArray实例，但属于新的一段数据
TypedArray.prototype.slice;

// 用于将参数转为一个TypedArray实例
TypedArray.of();

// 接受一个可遍历的数据结构（比如数组）作为参数，返回一个基于这个结构的TypedArray实例
TypedArray.from();
```

## DataView

最后就是`DataView`，它的方法较多，但都是大同小异。

> 重点：默认情况下，DataView 的 get 方法使用大端字节序解读数据，如果需要使用小端字节序解读，必须在 get 方法的第二个参数指定 true。

用一个例子说明一下，记住 `get` 方法的参数都是一个字节序号，不是字节大小，字节大小要看使用的什么方法。

```js
const uint8 = Uint8Array.from([1, 2, 3, 4]);
const view = new DataView(uint8.buffer);

// 从第 1 个字节读取一个8位无符号整数等于 1，这没问题, 单个字节也和用什么字节序无关
view.getUint8(0) === 1;

// 从第 1 个字节读取 2 个字节无符号整数呢？
// 那就是读取了[1, 2]
// 1 的二进制为 0b00000001, 2 的二进制为 0b00000010

// 假如是大端字节序，那就是1在前2在后为：0b0000000100000010
view.getUint16(0) === 0b000000001000000010;
view.getUint16(0) === 258;

// 假如是小端字节序，那就是2在前1在后为：0b0000001000000001
view.getUint16(0, true) === 0b0000001000000001;
view.getUint16(0, true) === 513;
```

还是那句话，机器运算的时候都是看二进制的，只是输出的时候是十进制而已，那么其他方法都可以举一反三了，也从这里可以看出，使用哪种字节序来读取数据，全依赖于当初那个人是以什么字节序写入数据而已，要怎么知道？看对应的规范文档吧。

> 重点：set 方法，接受两个参数，第一个参数是字节序号，表示从哪个字节开始写入，第二个参数为写入的数据。对于那些写入两个或两个以上字节的方法，需要指定第三个参数，false 或者 undefined 表示使用大端字节序写入，true 表示使用小端字节序写入。

再用一个例子说明一下

```js
const uint8 = Uint8Array.from([1, 2, 3, 4]);
const view = new DataView(uint8.buffer);

// 使用大端字节序，在第一位写入 1 个字节的 8 位无符号整数
view.setUint8(0, 2, false);
// 此时uint8为 [2, 2, 3, 4]

// 使用大端字节序，在第三位写入 2 个字节的 16 位无符号整数
view.setUint16(2, 256, false);
// 此时uint8为 [2, 2, 1, 0]，为什么第三、四位变成[1, 0]自己思考

// 使用小端字节序，在第三位写入 2 个字节的 16 位无符号整数
view.setUint16(2, 256, true);
// 此时uint8为 [2, 2, 0, 1]，为什么第三、四位变成[0, 1]自己思考
```
