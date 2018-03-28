### 参考
[https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)

### 构造函数
FileReader()：返回一个新构造的FileReader

### 实例属性
fileReader.error：一个DOMException，表示在读取文件时发生的错误

fileReader.readyState：表示FileReader状态的数字

fileReader.result：文件的内容。该属性仅在读取操作完成后才有效，数据的格式取决于使用哪个方法来启动读取操作

### 事件处理
fileReader.onabort：处理abort事件。该事件在读取操作被中断时触发

fileReader.onerror：处理error事件。该事件在读取操作发生错误时触发

fileReader.onload：处理load事件。该事件在读取操作完成时触发

fileReader.onloadstart：处理loadstart事件。该事件在读取操作开始时触发

fileReader.onloadend：处理loadend事件。该事件在读取操作结束时（要么成功，要么失败）触发

fileReader.onprogress：处理progress事件。该事件在读取Blob时触发

### 实例方法
fileReader.abort()：中止读取操作。在返回时，readyState属性为DONE

fileReader.readAsArrayBuffer()：开始读取指定的 Blob中的内容, 一旦完成, result 属性中保存的将是被读取文件的 ArrayBuffer 数据对象

fileReader.readAsBinaryString()：开始读取指定的Blob中的内容。一旦完成，result属性中将包含所读取文件的原始二进制数据。

fileReader.readAsDataURL()：开始读取指定的Blob中的内容。一旦完成，result属性中将包含一个data: URL格式的字符串以表示所读取文件的内容。

fileReader.readAsText()：开始读取指定的Blob中的内容。一旦完成，result属性中将包含一个字符串以表示所读取的文件内容。
