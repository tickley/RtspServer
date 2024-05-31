# RtspServer

项目介绍
-
* C++11实现的RTSP服务器和推流器。

项目Demo
-
* [DesktopSharing](https://github.com/PHZ76/DesktopSharing): 抓取屏幕和麦克风的音视频数据，编码后进行RTSP转发和推流。

目前情况
-
* 支持 Linux平台。
* 支持 H264, H265, G711A, AAC 四种音视频格式的转发。
* 支持同时传输音视频。
* 支持单播(RTP_OVER_UDP, RTP_OVER_RTSP), 组播。
* 支持心跳检测(单播)。
* 支持RTSP推流(TCP)。
* 支持摘要认证(Digest Authentication)。

编译环境
-
* Linux: gcc 10.1

整体框架
-
![image](https://github.com/PHZ76/RtspServer/blob/master/pic/1.pic.JPG) 

如何使用
-
* 数据流 v4l2 --> rkmpp_encode --> H264/H265 --> rtsp
* rtsp_camera 支持RK3566 RK3568 RK3588 其他芯片的视频编码模块
```
./buid-linux_RK3566_RK3568.sh
./install/rtsp_camera -I /dev/video11 -w 1920 -h 1080
```
