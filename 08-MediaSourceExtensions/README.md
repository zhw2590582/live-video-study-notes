## 媒体源扩展

- [MDN Web Docs - MSE API](https://developer.mozilla.org/zh-CN/docs/Web/API/Media_Source_Extensions_API)
- [MDN Web Docs - 为 MSE 做资源格式转换](https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API/Transcoding_assets_for_MSE)
- [W3C - MSE 字节流格式](https://www.w3.org/TR/mse-byte-stream-format-isobmff/)
- [检测 MP4 资源是否支持 MSE](http://nickdesaulniers.github.io/mp4info/)
- [MP4 结构在线解析](http://mp4parser.com/)
- [无 Flash 时代，让直播拥抱 H5（MSE 篇）](https://www.villainhr.com/page/2017/10/10/%E6%97%A0%20Flash%20%E6%97%B6%E4%BB%A3%EF%BC%8C%E8%AE%A9%E7%9B%B4%E6%92%AD%E6%8B%A5%E6%8A%B1%20H5%EF%BC%88MSE%E7%AF%87%EF%BC%89)

其实对于 `MSE` 的接口并不复杂，重点在于理解 `MediaSource` 和 `SourceBuffer` 两个概念，难就难在怎么构造出符合 `MSE` 的字节流，目前最理想的字节流格式就是 `H264` 和 `AAC` 组成的封装格式 `Fragmented MP4`，也就是简称的 `FMP4`，而且还要考虑诸多兼容问题，坑会比较多，所以在这之前要熟悉上面链接里的 `MSE` 概念。

参考网上的例子来操作一下：

- [https://html5-demos.appspot.com/static/media-source.html](https://html5-demos.appspot.com/static/media-source.html)
- [http://nickdesaulniers.github.io/netfix/demo/bufferAll.html](http://nickdesaulniers.github.io/netfix/demo/bufferAll.html)

首先准备好一个 `FMP4`，尝试在整个 `FMP4` 下载完成后再开始播放：

- [加载完再播放](http://zhw2590582.github.io/live-video-study-notes/mse-bufferAll.html)

然后尝试边加载边播放的简单例子，方法很多，我这里是通过`ReadableStreamDefaultReader`读取流：

- [边加载边播放](http://zhw2590582.github.io/live-video-study-notes/mse-bufferStream.html)

如上所见，`MSE` 不关心数据是怎么来的，只关心你给他的数据是可以被解析的就行，他只负责按照一定的规则，把数据解析并传输到 `video` 对象，至于后续怎么操作视频那也是 `video` 对象的事。
