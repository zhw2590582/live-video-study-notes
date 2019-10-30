## 音视频概念

- [在线查看视频信息：mediainfo.js - shows information about media files](https://mediainfo.js.org/)
- [在线视频格式转换：convert anything to anything](https://cloudconvert.com/)

音视频开发总会遇到很多新名词或新概念，下面是参考了上面的`mediainfo.js`整理出经常接触到的基础概念，以一个`MP4`为例，大部分解释来自搜索引擎。

### 视频

##### Format (格式)

视频常见编码格式有`H264(AVC)`、`H265(HEVC)` `VP8` `VP9`等。

##### Codecs (编解码器)

常见有`H.264`、`MPEG-4`、`DivX`、`MPEG-2`、`HEVC（H.265）`等。

##### Format profile (格式设定)

这里一般指的是两个属性：`profile` 和 `level`，是视频比较重要也比较复杂的概念，`profile` 是用来描述视频压缩特性的，`profile` 越高，就说明采用了越高级的压缩特性，`level` 是一组特定的约束，表示一个 `profile` 所需的解码性能。例如，`profile` 中的支持 `level` 指定了解码器可能使用的最大图像分辨率、帧率和比特率。一个符合给定 `level` 的解码器必须能够解码为该 `level` 和所有低 `level` 编码的所有比特流。

- [https://en.wikipedia.org/wiki/Advanced_Video_Coding#Profiles](https://en.wikipedia.org/wiki/Advanced_Video_Coding#Profiles)
- [https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels](https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels)

##### Codec ID（编码 ID）

其实就是编码器，下面有具体介绍：

[https://wiki.whatwg.org/wiki/Video_type_parameters](https://wiki.whatwg.org/wiki/Video_type_parameters)

##### Video Resolution（视频分辨率）

在视频处理和分发领域，图像或视频内容的通用术语“分辨率”通常定义总图像尺寸，以水平像素和垂直像素的数量来衡量。

![Resolution](./Resolution.png)

- [https://en.wikipedia.org/wiki/Display_resolution](https://en.wikipedia.org/wiki/Display_resolution)

##### Aspect Ratio（长宽比）

视频的长宽比描述了图像的宽度和高度之间的比例关系。如今，最常见的宽高比可能是 `16：9`（宽屏）格式。对于`16：9`的显示，这将是`16/9` = `1.78`，或也称为`1.78：1`。

![Aspect_Ratio](./Aspect_Ratio.jpg)

##### Bit rate (比特率)

字面理解就是每秒处理的位数，单位是`bit/s`，其中`8bit`等于`1kb`比特率是每秒的位数。它通常确定视频和音频文件的大小和质量：比特率越高，质量越好，文件大小也越大，因为文件大小 `=` 比特率 `x` 持续时间。

##### Frame rate (帧率）

视频的帧率定义了在有限的时间内将显示多少个连续图像，从而在观看者处产生运动图像感知，帧速率以每秒帧数（FPS）表示。

- [https://en.wikipedia.org/wiki/Frame_rate](https://en.wikipedia.org/wiki/Frame_rate)

##### Bit depth（颜色位深）

这是二进制数，代表每个颜色成分的可能值的总数，位数越多，信号的深度可能越大。例如位深是`8bit`位，颜色空间是`RGB`的话，每个像素点有三个值组成，每个值都是`8bit`，那么一个像素点有`24bit`，也就是`3`字节。

##### Color space（颜色空间）

可以用信号的颜色编码表示的可能色域例如：`RGB`，`YUV`，`Y'CrCb`。

##### Chroma subsampling（色度二次采样）

通过不同的采样方式减少每个像素的位数来减少色彩信息，但会浪费色彩空间例如：`4：4：4`、`4：2：2`、`4：2：0`。

- [一文读懂 YUV 的采样与格式](https://glumes.com/post/ffmpeg/understand-yuv-format/)
- [https://en.wikipedia.org/wiki/Chroma_subsampling](https://en.wikipedia.org/wiki/Chroma_subsampling)

##### 请问：一个分辨率为`1080p`，帧率是`60fps`，色彩空间是`YUV`，色度二次采样为`4：2：2`，颜色位深为`10bit`的未压缩视频，体积有多大？

- 首先一帧的像素点个数为：`1920 * 1080 = 2073600`
- 每秒的像素点个数为：`2073600 * 60 = 124416000`
- `Y`的采样比特大小为：`124416000 * 10 = 1244160000bit`
- `U`的采样比特大小为：`124416000 * 10 / 2 = 622080000bit`
- `V`的采样比特大小为：`124416000 * 10 / 2 = 622080000bit`
- 总体积为：`1244160000 + 622080000 + 622080000 = 2488320000bit`
- `2488320000bit`约等于`2.49G`

### 音频

### 字幕
