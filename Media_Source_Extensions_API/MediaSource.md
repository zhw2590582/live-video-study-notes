### 参考
[https://developer.mozilla.org/zh-CN/docs/Web/API/MediaSource](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaSource)

### 构造函数
MediaSource()：构造并且返回一个新的MediaSource的空对象

### 实例属性
mediaSource.sourceBuffers：返回一个SourceBufferList 对象，包含了这个MediaSource的SourceBuffer的对象列表

mediaSource.activeSourceBuffers：返回一个 SourceBufferList 对象，包含了这个MediaSource.sourceBuffers中的SourceBuffer 子集的对象—即提供当前被选中的视频轨 (video track)，启用的音频轨 (audio tracks) 以及显示/隐藏的字幕轨 (text tracks) 的对象列表。

mediaSource.readyState：返回一个包含当前MediaSource状态的集合，即使它当前没有附着到一个media元素

mediaSource.duration：获取和设置当前正在推流媒体的持续时间。

### 实例方法
mediaSource.addSourceBuffer()：创建一个带有给定MIME类型的新的 SourceBuffer 并添加到 MediaSource 的 SourceBuffers 列表。

mediaSource.removeSourceBuffer()：删除指定的SourceBuffer 从这个MediaSource对象中的 SourceBuffers列表。

mediaSource.endOfStream()：表示流的结束。

### 静态方法
MediaSource.isTypeSupported()：返回一个 Boolean 值表明给定的MIME类型是否被当前的浏览器支持——这意味着是否可以成功的创建这个MIME类型的SourceBuffer 对象