## 1 文件播放命令

1.1 Read yuv file and play

> ` gst-launch-1.0 filesrc location="/home/xyk/Documents/CLionProjects/OMSLinuxSample/1280x720_60_FourPeople.yuv" ! video/x-raw,format=I420 !  videoparse width=1280 height=720 framerate=60 ! xvimagesink`     

1.2 Read the camera and play

> `gst-launch-1.0 v4l2src ! vidoeconvert ! xvimagesink //摄像头`  

1.3 Read the yuv file and play in the peer client

> `gst-launch-1.0 filesrc location="/home/xyk/Documents/CLionProjects/OMSLinuxSample/1280x720_60_FourPeople.yuv" blocksize=1382400 ! webrtc peerserver="http://localhost:8095" id=11 peerid=12 width=1280 height=720 fps=60`
> 
> 通过gstreamer把yuv文件流传送到peer端

1.4 Read  h264 file to analytics

> `gst-launch-1.0 filesrc location="./640x480_30_800_source.h264" ! h264parse ! avdec_h264 ! facerecognition width=640 height=480 ! xvimagesink`

1.5 Read yuv file to analytics

> `gst-launch-1.0 filesrc location="./1280x720_60_FourPeople.yuv" ! video/x-raw,format=I420 ! videoparse width=1280 height=720 framerate=60 ! facerecognition width=1280 height=720 ! xvimagesink`

## 

## 2 视频数据格式

##### 2.1 概述

>        一般来说，直接采集到的视频数据是RGB24格式，RGB24一帧的大小size=width×heigth×3Bit，RGB32=width×height×4，如果是I420（即YUV标准格式4:2:0）的数据量是size=width×height×1.5Bit。
>     
>        在采集到RGB24数据后，需要对这个格式的数据进行第一次压缩。即将图像的颜色空间由RGB2YUV。因为，X264在进行编码的时候需要标准的YUV（4：2：0）。经过第一次数据压缩后RGB24－>YUV（I420）。这样，数据量将减少一半。同样，如果是RGB24－>YUV（YV12），也是减少一半。但是，虽然都是一半，如果是YV12的话效果就有很大损失。然后，经过X264编码后，数据量将大大减少。将编码后的数据打包，通过RTP实时传送。到达目的地后，将数据取出，进行解码。完成解码后，数据仍然是YUV格式的，所以，还需要一次转换，这样windows的驱动才可以处理，就是YUV2RGB24

## 3 小知识

- `pip install matplotlib -i https://mirrors.aliyun.com/pypi/simple/`   使用国内镜像安装会较快
- gerrit push: `git push origin HEAD:refs/for/master` 
- P2P server
  
  signaling server
  
  `/home/xyk/Documents/P2Pnew/CS_WebRTC_Conference_Server_Peer.v4.2/PeerServer-Release-4.2 $ node peerserver.js`  
  
  httpserver
  
  `/home/xyk/Documents/P2Pnew/owt-client-javascript/dist/samples/p2p`
