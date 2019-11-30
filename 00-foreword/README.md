## 前言

我觉得可以把音视频处理看做学习前端技术的一个领域细分，现在前端各种框架日新月异学无止境，或许可以回过头来研究一下数据最底层的知识，而且视频直播是一种很酷很好玩的东西，但受制于浏览器环境，纯`JS`（`NodeJS`不在话题之内）对于音视频领域的作用其实很有限，那么以现在的前端技术能对音视频做些什么，在这之前可以先看看雷大神的这篇入门文章：

[[总结]视音频编解码技术零基础学习方法](https://blog.csdn.net/leixiaohua1020/article/details/18893769)

首先是音视频原始信息的采集，就是最简单的打开摄像头/麦克风后所拿到的原始数据。其中视频的原始数据格式就是常见的`RGB`或者`YUV`，`RGB`大家都很熟悉，`YUV`会复杂一些而且根据采样方式不一样又会分出不同的类型，具体需要查一下资料理解一下。音频的原始数据就是`PCM`，也需要查一下资料，而且我可以很肯定的说，音频处理远远的难于视频处理。

前端可以使用`MediaDevices.getUserMedia`接口打开摄像头/麦克风:

[MDN Web Docs - MediaDevices.getUserMedia()](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)

你会发现上面这个接口很容易的就能实现了一个摄像头到浏览器的实时的播放器，但前端又怎么拿到中间传输的原始视频数据呢？这里有一个API叫`MediaRecorder`专门记录媒体流的，通过它可以拿到从摄像头进来的原始音视频字节流：

[MDN Web Docs - MediaRecorder](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaRecorder)

但有时候我们看不懂音视频字节流，我们只想拿到最直接的视频图像数据怎么办，这就轮到`canvas`出场了，因为`canvas`直接的`ctx.drawImage`方法可以直接绘制视频的某一帧，那我可以每秒截取`24`次，然后再用`ctx.getImageData`获取到`RGB`值，那也就可以从把`RGB`转换成`YUV`了，但不得不说这样做又繁琐效率又低下，没什么实际用起来的业务用途。

[MDN Web Docs - 使用 canvas 处理视频](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Manipulating_video_using_canvas)

拿到原始数据之后就是压缩编码啦，因为原始数据实在太大了，例如视频数据编码成`h264`或者`h265`，音频数据编码成`aac`或者`mp3`，这些都可以称作裸流，实际上通过摄像头进来的音视频数据已经被压缩过了，用纯`JS`实现软编码过程是非常困难的，至少目前没有这种东西，能用的方法就是把其他语言如`C`或者`C++`的现成编码器（如`FFmpeg`）转换成浏览器能运行的`WebAssembly`格式（文件体积通常很大），再配合`Worker`进行编码是最好的方法，但这种高密集的编码运算不适合在浏览器里运行，所有也没什么实际用起来的业务用途。

- [Github - Kagami/ffmpeg.js](https://github.com/Kagami/ffmpeg.js)
- [Github - bgrins/videoconverter.js](https://github.com/bgrins/videoconverter.js)

接着就是推流到服务器，常见的方法有`WebRTC`、`websocket`和`RTMP`，其中使用`RTMP`是各大平台目前视频推流是目前最主流的，但浏览器要使用`RTMP`就要安装`Flash`插件，现在看来明显不合理，用`websocket`推流见得不多，而`WebRTC`属于新技术且还没发展成熟，所以先不谈及。假如不用网页做推流的话，最流行的软件应该就是开源的`OBS`了。

- [Github - obsproject/obs-studio](https://github.com/obsproject/obs-studio)

接着就是服务器处理接收到的流，这个专门的流媒体服务器需要把音视频数据封装成浏览器能播放的格式如`mp4`、`ts`和`flv`等等，嫌麻烦可以用第三方的云服务，一劳永逸。

服务器处理完数据之后就是想办法发送到浏览器进行播放，这就要用到不同的直播或点播协议，如`HLS`、`RTMP`、`HTTP-FLV`和`WebSocket`等等。

前端能做的就是发起协议的连接，当服务器和浏览器建立了连接，数据就会传过来，浏览器就会根据不同的协议来`解协议`，但这一步是浏览器底层做的，前端也无法干预。

`解协议`出来的数据就是上面的封装格式数据如`mp4`、`ts`和`flv`，现在就是想办法去播放这些数据，那就是使用`HTML`的`video`标签播放，对于常规的点播来说，就是非常简单的给`video`标签添加`src`地址就可以了，但问题在于现在浏览器只支持`mp4`、`ogg`和`webm`格式，像`ts`和`flv`这种格式是没法直接播放的，但你会发现`mp4`、`ts`和`flv`的音视频裸流格式都是普遍的`h264`和`aac`，只是封装方式不一样，我们可以把`ts`和`flv`解封装拿到音视频数据再重封装成我们想要的`MP4`这是可行的，那就有了流行的工具可以做到如`hls.js`和`flv.js`就是干这个事的:

- [Github - video-dev/hls.js](https://github.com/video-dev/hls.js)
- [Github - bilibili/flv.js](https://github.com/bilibili/flv.js)

但是你会发现点播没问题，但直播的话就不是直接给`video`标签添加`src`地址就能解决的（除了`ios`原生支持的`m38u`地址），因为直播播放的是一个源源不断的数据流，你要不断的给`video`标签发送音视频数据才行，为了解决这个问题就有了`Media Source Extensions`接口专门给`video`发送数据流用的，但目前手机端尚未普及该接口。当然，上面的`hls.js`和`flv.js`都是基于`Media Source Extensions`实现的，所以也是支持直播的。

[MDN Web Docs - Media_Source_Extensions_API](https://developer.mozilla.org/zh-CN/docs/Web/API/Media_Source_Extensions_API)

当`video`拿到了封装的数据，就可以解封装成`h264`和`aac`，然后就是解码到视频的原始数据`RGB`或者`YUV`，音频的原始数据`PCM`，拿到原始数据之后就是做音视频同步，输送到硬件去播放，这一步是前端无法干预到的硬解码。

有硬解码也有软解码，上面提到的解协议之后拿到的数据，我也可以不用`video`和`Media Source Extensions`进行播放，我们可以自己把`ts`和`flv`软解码到视频的原始数据`RGB`或者`YUV`和音频的封装数据`aac`或者`mp3`，然后视频通过`canvas`播放，音频通过`AudioContext`播放，但这和上面软编码一样，纯`JS`也很难实现视频解码，最好方法把现成的解码器转换成浏览器能运行的`WebAssembly`格式，再配合`Worker`进行解码。软解码更可控更能实现自己想要的效果，但效率不高所以也没有普及。为什么不把音频数据也软解码到`PCM`？那是因为浏览器自带音频解码接口了，没必要再实现一次。下面就是对于软解码的一些方案：

- [Github - mbebenita/Broadway](https://github.com/mbebenita/Broadway)
- [Github - phoboslab/jsmpeg](https://github.com/phoboslab/jsmpeg)

总结下来，前端对于流媒体处理的最有有用的部分其实是原始数据的解封装和重封装，对于用到什么协议我们并不关心，我们只关心拿到的是什么数据，目标要转换成什么样的数据，并且最终能音视频同步的播放出来，以后的文章都会围绕着这个话题进行展开，会涉及到平常前端接触不到的知识，可以坚持的话就看下去吧。其实可以把这种做法看成技术开发向浏览器妥协的一种做法，搞出这么多东西出来，到时浏览器厂商来了句：我也可以原生直接播放`ts`和`flv`啦！那不就尴尬了。
