## 媒体源扩展

- [MDN Web Docs - MSE API](https://developer.mozilla.org/zh-CN/docs/Web/API/Media_Source_Extensions_API)
- [MDN Web Docs - 为 MSE 做资源格式转换](https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API/Transcoding_assets_for_MSE)
- [W3C - MSE 字节流格式](https://www.w3.org/TR/mse-byte-stream-format-isobmff/)
- [检测 MP4 资源是否支持 MSE](http://nickdesaulniers.github.io/mp4info/)

其实对于 `MSE` 的接口并不复杂，重点在于理解 `MediaSource` 和 `SourceBuffer` 两个概念，难就难在怎么构造出符合 `MSE` 的字节流，目前最理想的字节流格式就是 `H264` 和 `AAC` 组成的封装格式 `Fragmented MP4`，也就是简称的 `FMP4`，而且还要考虑诸多兼容问题，坑会比较多，下面主要分析怎么构造出 `FMP4` 字节流，所以在这之前要熟悉上面链接里的 `MSE` 概念。

参考网上的例子来操作一下：

- [https://html5-demos.appspot.com/static/media-source.html](https://html5-demos.appspot.com/static/media-source.html)
- [http://nickdesaulniers.github.io/netfix/demo/bufferAll.html](http://nickdesaulniers.github.io/netfix/demo/bufferAll.html)

首先准备好一个 `FMP4`，尝试在整个 `FMP4` 下载完成后，再开始播放，这和直接在`video`标签添加`src`属性没什么差别：

- [加载完再播放](http://zhw2590582.github.io/live-video-study-notes/mse-bufferAll.html)

然后尝试边加载边播放的例子，是通过`ReadableStreamDefaultReader`读取流，或者通过`Header Range`请求头读取分段也可以：

- [边加载边播放](http://zhw2590582.github.io/live-video-study-notes/mse-bufferStream.html)
