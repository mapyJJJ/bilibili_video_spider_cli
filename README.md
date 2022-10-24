#### bilibili视频下载工具

(针对网页端使用者或者需要下载指定清晰度的视频 ，手机端app部分视频提供了下载分享功能，但是无法指定视频下载质量，可以使用此工具代替下载)

---

`python >= 3.10`

##### 使用方法
```
usage: spider.py [-h] [--url URL] [--urlfile URLFILE] [--qn QN] [--type TYPE] [--cookie COOKIE] [--cookiefile COOKIEFILE] [--outputdir OUTPUTDIR]

b站视频下载工具

options:
  -h, --help            show this help message and exit
  --url URL             视频地址链接
  --urlfile URLFILE     批量下载对应文件中的所有地址，每个链接一行
  --qn QN               分辨率大小 120: "4K 超清", 116: "1080P 60帧", 80: "1080P 高清", 64: "720P 高清", 32: "480P 清晰", 16: "360P 流畅",
  --type TYPE           保存文件类型 mp4 | flv， 有的视频mp4格式获取到的分辨率较低
  --cookie COOKIE       账号的cookie，注意传递时要用双引号包起来，但不建议直接作为参数在此处传递
  --cookiefile COOKIEFILE
                        读取文本中的cookie值，为了安全请将cookie值写入某个文件中，由程序自行读取
  --outputdir OUTPUTDIR
                        将视频存入指定的文件夹路径中
```
                        
---

##### 更新日志
22.09: 
- 完成调研，实现基础逻辑和命令行指令，从视频所在页面的连接 通过代码获取 最终视频地址，并爬取保存
- 修复视频重复下载的问题，对page uri 和 title 进行hash 去重
- 使用rich进度条 展示下载进度
- 修复大视频下载中断的问题，重试，视频分片下载

22.10:
- 修复无法部分类型的视频(番剧，电影，纪录片)无法下载的问题，增加解析逻辑
- 反爬处理，视频cdn地址出现防盗链，下载出现403，download request header 增加 referer
- 反爬处理，cookie中的一个key，CURRENT_QUALIT，比接口所需的qn值优先级更高，获取对应清晰度时需要同时更改cookie
- 反爬处理，player_info接口无法获取全部的清晰度视频地址，最高只到 1080p，发现需要设置 fnval 参数，
            fnval从cookie中获取，但是发现接口的返回值结构发生变化，且无法指定视频文件格式，研究后发现只需要将fnval加1，后续一切正常

持续更新.....
                        
---


##### 使用示例

（1）例如需要下载下图中的4k质量的视频
![image](https://user-images.githubusercontent.com/35096746/197456492-84999628-f4db-476a-8eeb-b0a05ca675f2.png)


（2）创建一个文件写入自己的账号cookie （例如写入到cookie.txt 中）
 说明: 能下载的视频清晰度取决于你自己账号的权限（未登录，登录，登录且是会员 ， 会员可以下载最高清晰度的视频），并非破解或者第三方盗版，只是拿你自己的账号，办你能办但平台不让你办的事情
 执行命令下载视频
 ![image](https://user-images.githubusercontent.com/35096746/197458878-b9e5ca89-684e-4564-a27d-583b84e3f3fe.png)

（3）查看视频已经下载到本地
![image](https://user-images.githubusercontent.com/35096746/197459127-91deb39f-d9ab-4d4d-818b-ae29f703523f.png)

