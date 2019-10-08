## 前言

我觉得可以把音视频处理看做学习前端技术的一个领域细分，现在前端各种框架日新月异学无止境，或许可以回过头来研究一下数据最底层的知识，而且视频直播是一种很酷很好玩的东西，但受制于浏览器环境，纯`JS`（`NodeJS`不在话题之内）对于音视频领域的作用其实很有限，那么以现在的前端技术能对音视频做些什么，在这之前可以先看看雷大神的这篇入门文章：

[[总结]视音频编解码技术零基础学习方法](https://blog.csdn.net/leixiaohua1020/article/details/18893769)

首先是音视频原始信息的采集，就是最简单的打开摄像头/麦克风后所拿到的原始数据。其中视频的原始数据格式就是常见的`RGB`或者`YUV`，`RGB`大家都很熟悉，`YUV`会复杂一些而且根据采样方式不一样又会分出不同的类型，具体需要查一下资料理解一下。音频的原始数据就是`PCM`，也需要查一下资料，而且我可以很肯定的说，音频处理远远的难于视频处理。

前端可以使用`MediaDevices.getUserMedia`接口打开摄像头:

[MDN Web Docs - MediaDevices.getUserMedia()](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)

你会发现上面这个接口很容易的就能实现了一个摄像头到浏览器的实时的播放器，但前端又怎么拿到中间传输的原始视频数据呢？这就轮到`canvas`出场了，因为`canvas`直接的`ctx.drawImage`方法可以直接绘制视频的某一帧，那我可以每秒截取`24`次，然后再用`ctx.getImageData`获取到`RGB`值，那也就可以从把`RGB`转换成`YUV`了，但不得不说这样做又繁琐效率又低下，没什么实际用起来的业务用途。

[MDN Web Docs - 使用 canvas 处理视频](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Manipulating_video_using_canvas)
