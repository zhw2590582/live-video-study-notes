## 网页二进制接口

相关文档可以大概预览一下，不需要刻意记住。

- [MDN Web Docs - File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)
- [MDN Web Docs - Blob](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)
- [MDN Web Docs - Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API)
- [MDN Web Docs - FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)
- [MDN Web Docs - HTMLCanvasElement](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement)
- [MDN Web Docs - URL.createObjectURL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL)
- [MDN Web Docs - URL.revokeObjectURL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/revokeObjectURL)
- [MDN Web Docs - TextEncoder](https://developer.mozilla.org/zh-CN/docs/Web/API/TextEncoder/TextEncoder)

### 获取二进制数据

网页不像`Nodejs`，可以接触到二进制数据的情况并不多，简单概括下几种情况。

#### Ajax

```js
let xhr = new XMLHttpRequest();
xhr.open("GET", someUrl);
xhr.responseType = "arraybuffer";
xhr.onload = function() {
  let uint8 = new Uint8Array(xhr.response);
  console.log(uint8);
};
xhr.send();
```

#### Fetch

```js
fetch(someUrl)
  .then(function(response) {
    return response.arrayBuffer();
  })
  .then(function(arrayBuffer) {
    let uint8 = new Uint8Array(arrayBuffer);
    console.log(uint8);
  });
```

#### Websocket

```js
let socket = new WebSocket(someUrl);
socket.binaryType = "arraybuffer";
socket.onmessage = function(e) {
  let uint8 = new Uint8Array(e.data);
  console.log(uint8);
};
socket.send();
```

#### Canvas

```js
const canvas = document.getElementById("myCanvas");
const ctx = canvas.getContext("2d");
const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
const uint8ClampedArray = imageData.data;
```

#### FileReader

```js
const fileInput = document.getElementById("fileInput");
const file = fileInput.files[0];
const reader = new FileReader();
reader.readAsArrayBuffer(file);
reader.onload = function() {
  let uint8 = new Uint8Array(reader.result);
  console.log(uint8);
};
```
