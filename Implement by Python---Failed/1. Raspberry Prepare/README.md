# 树莓派准备工作
  
## 1. 硬件需求
  
- 最低要求是 RaspberryPi Zero W 以上，我用的是树莓派 3b。  
- 准备个树莓派用的电源，可以直接用准备给机器狗供电的电池，但是为了方便调试，建议还是用个 micro USB 的充电器比较好。  
- micro SD 卡一张，最低要 16G 以上，我使用的是 32G 的。另外确保你有个合适的读卡器。  
- 周围有自己作为管理员的 wifi 网络，否则需要有根网线，然后你的电脑也需要有可以连网线的接口。  
- 计算机一台。  

## 2. 树莓派操作系统  
  
Raspbian 是树莓派的官方操作系统，这个项目中我们会使用的是轻量化的操作系统 RaspbianLite。  
由于我们不是要用树莓派打造一台电脑，所以我们自然也不会准备额外的键盘，鼠标和显示器，那吗要如何安装树莓派的操作系统呢？  

### 第一步  
  
安装 PINN，这个软件可以帮助我们安装操作系统。  
下载地址：  
http://sourceforge.net/projects/pinn/files/pinn-lite.zip  
  
### 第二步  
  
我们需要专门的格式化软件去格式化我们的 SD 卡。为了确保不出问题，即使是新的 SD 卡，也建议进行格式化。  
推荐的专用格式化软件为：  
https://www.sdcard.org/downloads/formatter/  
  
- 首先下载下来，根据自己的系统选择对应版本就行，我的 Mac 也有对应适用的版本。  
- 然后安装。  
- 把 SD 卡查到电脑上。  
- 双击运行安装好的 SD Card Formatter。  
- 选到你的 SD 卡，一般默认已经选到了。
- 点击 Format 即可。  

### 第三步  
  
把之前下载的 pinn-lite.zip 文件里面的内容都解压缩到 SD 卡的根目录下。  
  
### 第四步  
  
因为我们要通过 Wi-Fi 远程控制我们的树莓派，所以有两个东西必不可少，一个就是开启远程控制的权限 SSH，另一个就是安装远程控制软件 VNC。  
只要做到这两点，我们即使没有鼠标，键盘和显示器，也可以愉快的玩耍树莓派啦！  
  
- 进入 SD 卡根目录，就是我们刚刚把压缩包里面的文件解压进去的地方。
- 找到 **recovery.cmdline** 这个文件，使用纯文本编辑器打开（比如 Sublime Text）。  
- 添加两个词：  
    - vncshare  
    - ssh  
- 然后保存文件。  
  
### 第五步  
  
为了让树莓派系统启动的时候自动开启 SSH，我们需要在 SD 卡根目录下新建一个空的文件，文件名为 **ssh**，里面内容空着，文件不需要有后缀名，也可以用纯文本编辑器新建该文件。  
  
### 第六步  
  
我们要连接 Wi-Fi，还需要告知树莓派无线网络的用户名和密码。  
  
- 打开 SD 卡根目录。  
- 新建纯文本文件 **wpa_supplicant.conf**  
- 文件内容如下：  
  
```
country=cn
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 scan_ssid=1
 ssid="YOUR_WIFI_SSID你的wifi用户名"
 psk="YOUR_WIFI_PASSWORD你的wifi密码"
}
```
  
- 最后别忘了保存文件！

