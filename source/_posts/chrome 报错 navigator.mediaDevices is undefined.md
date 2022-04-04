---
title: chrome 报错 navigator.mediaDevices is undefined
---
chrome 报错 navigator.mediaDevices is undefined
最近在开发一个摄像头项目（多人会议，需要摄像头~~）。然后同事的电脑调试好好的，到我这里就报错了，我的 chrome 版本一直都在最新的，为啥到我这反而还不兼容？

原来是以后的内容会越来越严格
chrome：想调用摄像头？可以啊，拿出你的https证书给我瞧瞧

## 解决问题

### 解决方法 1
通过相应参数启动 Chrome

比如我们调试的链接是:http://example.com。如果有多个网址，用,隔开
``` bash
$  --unsafely-treat-insecure-origin-as-secure="http://example.com"
```
加哪里呢？
![1](https://img-blog.csdnimg.cn/img_convert/891a5fd80f3aee3cd6502dc056ca78ff.png)

### 解决方法 2（比较推荐这个）
chrom 下
打开 chrome://flags/#unsafely-treat-insecure-origin-as-secure

选 enabled
填写需要调试的 URL，多个 URL 以,隔开
完全重启 chrome 后起效（改了之后下面也会有个 relaunch 按钮）
