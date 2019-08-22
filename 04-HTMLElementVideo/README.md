## 视频 DOM 元素

- [W3school - HTML 5 视频/音频参考手册](https://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)
- [MDN Web Docs - video](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/video)

`HTMLMediaElement`和`HTMLVideoElement`都是`video`元素的构造函数，网页端音视频播放的所有相关接口都是继承于他们，理解之后再写个播放器也是很简单的事情。

全部属性、方法和事件使用`chrome 76`测试是否支持

### 属性

| 属性                | 描述                                                       | 支持情况 |
| ------------------- | ---------------------------------------------------------- | -------- |
| audioTracks         | 返回表示可用音轨的 AudioTrackList 对象                     | 支持     |
| autoplay            | 设置或返回是否在加载完成后随即播放音频/视频                | 支持     |
| buffered            | 返回表示音频/视频已缓冲部分的 TimeRanges 对象              | 支持     |
| controller          | 返回表示音频/视频当前媒体控制器的 MediaController 对象     | 支持     |
| controls            | 设置或返回音频/视频是否显示控件（比如播放/暂停等）         | 支持     |
| crossOrigin         | 设置或返回音频/视频的 CORS 设置                            | 支持     |
| currentSrc          | 返回当前音频/视频的 URL                                    | 支持     |
| currentTime         | 设置或返回音频/视频中的当前播放位置（以秒计）              | 支持     |
| defaultMuted        | 设置或返回音频/视频默认是否静音                            | 支持     |
| defaultPlaybackRate | 设置或返回音频/视频的默认播放速度                          | 支持     |
| duration            | 返回当前音频/视频的长度（以秒计）                          | 支持     |
| ended               | 返回音频/视频的播放是否已结束                              | 支持     |
| error               | 返回表示音频/视频错误状态的 MediaError 对象                | 支持     |
| loop                | 设置或返回音频/视频是否应在结束时重新播放                  | 支持     |
| mediaGroup          | 设置或返回音频/视频所属的组合（用于连接多个音频/视频元素） | 支持     |
| muted               | 设置或返回音频/视频是否静音                                | 支持     |
| networkState        | 返回音频/视频的当前网络状态                                | 支持     |
| paused              | 设置或返回音频/视频是否暂停                                | 支持     |
| playbackRate        | 设置或返回音频/视频播放的速度                              | 支持     |
| played              | 返回表示音频/视频已播放部分的 TimeRanges 对象              | 支持     |
| preload             | 设置或返回音频/视频是否应该在页面加载后进行加载            | 支持     |
| readyState          | 返回音频/视频当前的就绪状态                                | 支持     |
| seekable            | 返回表示音频/视频可寻址部分的 TimeRanges 对象              | 支持     |
| seeking             | 返回用户是否正在音频/视频中进行查找                        | 支持     |
| src                 | 设置或返回音频/视频元素的当前来源                          | 支持     |
| startDate           | 返回表示当前时间偏移的 Date 对象                           | 支持     |
| textTracks          | 返回表示可用文本轨道的 TextTrackList 对象                  | 支持     |
| videoTracks         | 返回表示可用视频轨道的 VideoTrackList 对象                 | 支持     |
| volume              | 设置或返回音频/视频的音量                                  | 支持     |

### 方法

| 方法           | 描述                                    | 支持情况 |
| -------------- | --------------------------------------- | -------- |
| addTextTrack() | 向音频/视频添加新的文本轨道             | 支持     |
| canPlayType()  | 检测浏览器是否能播放指定的音频/视频类型 | 支持     |
| load()         | 重新加载音频/视频元素                   | 支持     |
| play()         | 开始播放音频/视频                       | 支持     |
| pause()        | 暂停当前播放的音频/视频                 | 支持     |

### 事件

| 事件           | 描述                                         | 支持情况 |
| -------------- | -------------------------------------------- | -------- |
| abort          | 当音频/视频的加载已放弃时                    | 支持     |
| canplay        | 当浏览器可以播放音频/视频时                  | 支持     |
| canplaythrough | 当浏览器可在不因缓冲而停顿的情况下进行播放时 | 支持     |
| durationchange | 当音频/视频的时长已更改时                    | 支持     |
| emptied        | 当目前的播放列表为空时                       | 支持     |
| ended          | 当目前的播放列表已结束时                     | 支持     |
| error          | 当在音频/视频加载期间发生错误时              | 支持     |
| loadeddata     | 当浏览器已加载音频/视频的当前帧时            | 支持     |
| loadedmetadata | 当浏览器已加载音频/视频的元数据时            | 支持     |
| loadstart      | 当浏览器开始查找音频/视频时                  | 支持     |
| pause          | 当音频/视频已暂停时                          | 支持     |
| play           | 当音频/视频已开始或不再暂停时                | 支持     |
| playing        | 当音频/视频在已因缓冲而暂停或停止后已就绪时  | 支持     |
| progress       | 当浏览器正在下载音频/视频时                  | 支持     |
| ratechange     | 当音频/视频的播放速度已更改时                | 支持     |
| seeked         | 当用户已移动/跳跃到音频/视频中的新位置时     | 支持     |
| seeking        | 当用户开始移动/跳跃到音频/视频中的新位置时   | 支持     |
| stalled        | 当浏览器尝试获取媒体数据，但数据不可用时     | 支持     |
| suspend        | 当浏览器刻意不获取媒体数据时                 | 支持     |
| timeupdate     | 当目前的播放位置已更改时                     | 支持     |
| volumechange   | 当音量已更改时                               | 支持     |
| waiting        | 当视频由于需要缓冲下一帧而停止               | 支持     |
