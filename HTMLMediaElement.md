[https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLMediaElement](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLMediaElement)
[http://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp](http://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)

#### 属性
audioTracks：返回表示可用音轨的 AudioTrackList 对象
autoplay：设置或返回是否在加载完成后随即播放音频/视频
buffered：返回表示音频/视频已缓冲部分的 TimeRanges 对象
controller：返回表示音频/视频当前媒体控制器的 MediaController 对象
controls：设置或返回音频/视频是否显示控件（比如播放/暂停等）
controlsList：未知
crossOrigin：设置或返回音频/视频的 CORS 设置
currentSrc：返回当前音频/视频的 URL
currentTime：设置或返回音频/视频中的当前播放位置（以秒计）
defaultMuted：设置或返回音频/视频默认是否静音
defaultPlaybackRate：设置或返回音频/视频的默认播放速度
duration：返回当前音频/视频的长度（以秒计）
ended：返回音频/视频的播放是否已结束
error：返回表示音频/视频错误状态的 MediaError 对象
loop：设置或返回音频/视频是否应在结束时重新播放
mediaGroup：设置或返回音频/视频所属的组合（用于连接多个音频/视频元素）
muted：设置或返回音频/视频是否静音
networkState：返回音频/视频的当前网络状态
paused：设置或返回音频/视频是否暂停
playbackRate：设置或返回音频/视频播放的速度
preload：设置或返回音频/视频是否应该在页面加载后进行加载
readyState：返回音频/视频当前的就绪状态
seekable：返回表示音频/视频可寻址部分的 TimeRanges 对象
seeking：返回用户是否正在音频/视频中进行查找
sinkId：未知
src：设置或返回音频/视频元素的当前来源
srcObject：对象提供了一个与HTMLMediaElement关联的媒体源，这个对象通常是 MediaStream ，但根据规范可以是 MediaSource， Blob 或者 File
textTracks：返回表示可用文本轨道的 TextTrackList 对象
videoTracks：返回表示可用视频轨道的 VideoTrackList 对象
volume：设置或返回音频/视频的音量

#### 方法
addTextTrack()：向视频添加一个新的文本轨道
canPlayType()：检测浏览器是否能播放指定的音频/视频类型                        
captureStream()：未知
fastSeek()：直接寻找到给定的时间。
load()：重新加载音频/视频元素
pause()：暂停当前播放的音频/视频
play()：开始播放音频/视频
setMediaKeys()：未知
setSinkId()：未知

#### 事件
abort：当音频/视频的加载已放弃时
canplay：当浏览器可以播放音频/视频时
canplaythrough：当浏览器可在不因缓冲而停顿的情况下进行播放时
durationchange：当音频/视频的时长已更改时
emptied：当目前的播放列表为空时
encrypted：未知
ended：当目前的播放列表已结束时
error：当在音频/视频加载期间发生错误时
interruptbegin：未知
interruptend：未知
loadeddata：当浏览器已加载音频/视频的当前帧时
loadedmetadata：当浏览器已加载音频/视频的元数据时
loadstart：当浏览器开始查找音频/视频时
pause：当音频/视频已暂停时
play：当音频/视频已开始或不再暂停时
playing：当音频/视频在已因缓冲而暂停或停止后已就绪时
progress：当浏览器正在下载音频/视频时
ratechange：当音频/视频的播放速度已更改时
seeked：当用户已移动/跳跃到音频/视频中的新位置时
seeking：当用户开始移动/跳跃到音频/视频中的新位置时
stalled：当浏览器尝试获取媒体数据，但数据不可用时
suspend：当浏览器刻意不获取媒体数据时
timeupdate：当目前的播放位置已更改时
volumechange：当音量已更改时
waiting：当视频由于需要缓冲下一帧而停止

#### 当音频/视频处于加载过程中时，会依次发生以下事件：
loadstart
durationchange
loadedmetadata
loadeddata
progress
canplay
canplaythrough