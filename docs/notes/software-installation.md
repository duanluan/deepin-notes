# 软件安装

`Ctrl` `Alt` `T`打开终端：
```shell
# 更新 APT 软件包索引
sudo apt update
```

## 应用商店安装

- Microsoft Edge
- QQ
- 微信
- WPS Office For Linux 个人版
- KeePassXC
- 腾讯会议
- Another Redis Desktop Manager

## Free Download Manager

[Free Download Manager for Linux | Download](https://www.freedownloadmanager.org/zh/download-fdm-for-linux.htm) 下载 DEB 文件打开并安装。

## Spark Store 星火应用商店安装

在[下载 - 星火应用商店](https://www.spark-app.store/download_latest)中下载软件本体，打开 DEB 文件安装。 

- Snipaste
- Wine 运行器

## Geekbench 6 跑分

[Downloading Geekbench 6 for Linux](https://www.geekbench.com/download/linux/) 下载

```shell
tar zxvf Geekbench-6.4.0-Linux.tar.gz
cd Geekbench-6.4.0-Linux
./geekbench6
```

## Synology Drive Client

[下载中心 | 群晖科技 Synology Inc.](https://www.synology.cn/zh-cn/support/download) 下载 DEB 文件并打开安装。

## Git

```shell
sudo apt install git
```

创建 SSH Key：

参考 [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)。

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub
```

设置 Git 用户信息，否则 clone 时可能会报错`GnuTLS recv error (-110)`。

```shell
git config --global user.name "your_name"
git config --global user.email "your_email@example.com"
```

## Clash Verge

[Releases · clash-verge-rev/clash-verge-rev](https://github.com/clash-verge-rev/clash-verge-rev/releases) 下载 DEB 文件并打开安装。

## Brook

```shell
$ export http_proxy=127.0.0.1:7897
$ export https_proxy=127.0.0.1:7897
$ bash <(curl https://bash.ooo/nami.sh)
$ nami install brook

# 创建 brook 脚本，自定义目录
$ vim ~/workspaces/service/brook.service.sh

#!/bin/bash
# 查找包含 'brook wsclient' 的进程，并获取 PID
pids=$(ps aux | grep '[b]rook wsclient' | awk '{print $2}')
# 判断是否找到了 PID
if [ -n "$pids" ]; then
  for pid in $pids; do
    echo "正在终止 brook wsclient 进程 (PID: $pid)"
    kill "$pid"
  done
else
  echo "没有找到 brook wsclient 进程"
fi
# 启动 brook，具体命令看官方文档
/home/your_name/.nami/bin/brook client -s 1.2.3.4:9999 -p 123456 --socks5 127.0.0.1:1080


# 将 brook 脚本创建为 systemd 服务
$ sudo vim /etc/systemd/system/brook.service

[Unit]
Description=A cross-platform programmable network tool.
After=network.target

[Service]
ExecStart=bash /home/your_name/workspaces/service/brook.service.sh
Restart=always
RestartSec=5
StandardOutput=null
StandardError=null
#StandardError=file:/home/your_name/workspaces/service/brook_error.log
User=your_name

[Install]
WantedBy=multi-user.target

```

## proxychains4

安装 proxychains4：
```shell
sudo apt install proxychains4
```

在配置文件`/etc/proxychain4.conf`末尾 [ProxyList] 后注释默认代理并添加新代理。
```shell
sudo vim /etc/proxychain4.conf
```
```conf
[ProxyList]
socks5 127.0.0.1 7897
```

## nvm + Node.js + pnpm + nrm

[脚本安装 nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script)

```shell
# 代理下载安装脚本
proxychains4 wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh
# 替换安装脚本中 git clone 为 proxychains4 git clone
sed -i 's/command git clone/command proxychains4 git clone/g' install.sh
# 执行脚本
bash install.sh
# 生效新环境变量
source ~/.bashrc
# 安装 Node.js
nvm install 18
# 安装 pnpm
npm install -g pnpm
# 自动安装配置 pnpm
pnpm setup
source ~/.bashrc
# 安装 nrm
pnpm add -g nrm
# 查看所有镜像源
nrm ls
  npm ---------- https://registry.npmjs.org/
  yarn --------- https://registry.yarnpkg.com/
  tencent ------ https://mirrors.tencent.com/npm/
  cnpm --------- https://r.cnpmjs.org/
  taobao ------- https://registry.npmmirror.com/
  npmMirror ---- https://skimdb.npmjs.com/registry/
  huawei ------- https://repo.huaweicloud.com/repository/npm/
# 使用镜像源
nrm use cnpm
```

## JDK

[Java 8, 11, 17, 21, 23 Download for Linux, Windows and macOS](https://www.azul.com/downloads/?os=debian&architecture=x86-64-bit&package=jdk#zulu)

```shell
tar zxvf zulu21.40.17-ca-jdk21.0.6-linux_x64.tar.gz
sudo mkdir /opt/java
sudo mv zulu21.40.17-ca-jdk21.0.6-linux_x64 /opt/java/zulu21.40.17-ca-jdk21.0.6
# 末尾追加环境变量
$ vim ~/.bashrc
# jdk
export JAVA_HOME="/opt/java/zulu21.40.17-ca-jdk21.0.6"
export PATH=$JAVA_HOME/bin:$PATH

$ source ~/.bashrc
$ java -version
openjdk version "21.0.6" 2025-01-21 LTS
OpenJDK Runtime Environment Zulu21.40+17-CA (build 21.0.6+7-LTS)
OpenJDK 64-Bit Server VM Zulu21.40+17-CA (build 21.0.6+7-LTS, mixed mode, sharing)

```

## Gradle

[Gradle | Releases](https://gradle.org/releases/) 下载`binary-only`。

```shell
unzip gradle-7.6.4-bin.zip
sudo mkdir /opt/gradle
sudo mv gradle-7.6.4 /opt/gradle/
# 末尾追加环境变量
$ vim ~/.bashrc
# gradle
export GRADLE_HOME="/opt/gradle/gradle-7.6.4"
export PATH=$GRADLE_HOME/bin:$PATH

$ source ~/.bashrc
$ gradle -v

Welcome to Gradle 7.6.4!
……

```

## JetBrains IntelliJ IDEA

[下载 IntelliJ IDEA](https://www.jetbrains.com/zh-cn/idea/download/?section=linux)

[MIME 类型（MIME Type）完整对照表](https://mime.wcode.net/zh-hans/)

```shell
# 解压并移动到 /opt 下
tar zxvf ideaIU-2024.3.4.1.tar.gz
sudo mkdir /opt/jetbrains
sudo mv idea-IU-243.25659.59/ /opt/jetbrains/idea
# 创建快捷方式
sudo vim /usr/share/applications/idea.desktop

[Desktop Entry]
Name=IntelliJ IDEA Ultimate
Comment=The IDE for Professional Development in Java and Kotlin
GenericName=IDE
Exec=/opt/jetbrains/idea/bin/idea %F
Icon=/opt/jetbrains/idea/bin/idea.svg
Type=Application
# 禁用启动时进度通知
StartupNotify=false
# 与应用程序窗口关联的 WM_CLASS 属性
StartupWMClass=jetbrains-idea
Categories=TextEditor;Development;IDE;
MimeType=application/java;application/java-archive;application/java-byte-code;application/java-vm;
Keywords=idea;
```

## JetBrains WebStorm

[下载 WebStorm](https://www.jetbrains.com/zh-cn/webstorm/download/#section=linux)

```shell
# 解压并移动到 /opt 下
tar zxvf WebStorm-2024.3.4.tar.gz
sudo mkdir /opt/jetbrains
sudo mv WebStorm-243.25659.40/ /opt/jetbrains/webstorm
# 创建快捷方式
sudo vim /usr/share/applications/webstorm.desktop

[Desktop Entry]
Name=WebStorm
Comment=The JavaScript and TypeScript IDE by JetBrains
GenericName=IDE
Exec=/opt/jetbrains/webstorm/bin/webstorm %F
Icon=/opt/jetbrains/webstorm/bin/webstorm.svg
Type=Application
# 禁用启动时进度通知
StartupNotify=false
# 与应用程序窗口关联的 WM_CLASS 属性
StartupWMClass=jetbrains-webstorm
Categories=TextEditor;Development;IDE;
MimeType=application/xhtml+xml;text/javascript;text/css;
Keywords=webstorm;
```

## uTools

应用商店安装的无法打开。

[下载中心 - uTools 官网](https://www.u-tools.cn/download/)下载 DEB 文件并打开安装。

## RustDesk

[Releases · rustdesk/rustdesk](https://github.com/rustdesk/rustdesk/releases/)下载 DEB 文件并打开安装。

## VMware Workstation Pro

[如何在 Linux 上下载和安装 VMware Workstation Pro 免费版 - 系统极客](https://www.sysgeek.cn/install-vmware-workstation-pro-on-linux/)

[注册 Broadcom](https://profile.broadcom.com/web/registration) 账号，用邮箱作用户名登录。

[Free Downloads - Support Portal - Broadcom support portal](https://support.broadcom.com/group/ecx/free-downloads) 搜索“VMware Workstation Pro”后下载 Linux 版。

```shell
chmod +x VMware-Workstation-Full-17.6.3-24583834.x86_64.bundle
sudo ./VMware-Workstation-Full-17.6.3-24583834.x86_64.bundle
```

安装过程中“VMware's Customer Experience Improvement Program ("CEIP")”可以选 No。

安装 [open-vm-tools](https://github.com/vmware/open-vm-tools) 增强虚拟机：

```shell
sudo apt install open-vm-tools
```

## XMind

[免费下载 Xmind 思维导图 | Xmind 中文官方网站](https://xmind.cn/download/) 下载 DEB 文件并打开安装。

## 搜狗输入法

fcitx5 和 fcitx 冲突，要先卸载 fcitx5。

```shell
# 卸载 fcitx5
sudo apt purge fcitx5
sudo apt purge fcitx5-chinese-addons-data

# 安装 fcitx
sudo apt install fcitx
```

[搜狗输入法 linux](https://shurufa.sogou.com/linux) 下载 DEB 文件并打开安装。

注销或重启，`控制中心`-`键盘和语言`-`输入法`中就空了，只能通过开始菜单`输入法配置`管理。

## Apifox

[Apifox](https://apifox.com/) 下载 DEB 文件并打开安装。

## Navicat Premium

此处安装的是 Windows 版。

[Navicat | 下载 Navicat Premium Windows](https://www.navicat.com.cn/download/navicat-premium#windows)

Wine 运行器菜单栏`程序`-`安装更多Wine`：

![](assets/20250309230531.png)

菜单栏`Wine`-`安装常见字体`，左下角`WINE配置`-`字体商店`安装 1~5 的字体。

左下角`WINE配置`-`配置容器`，调整`应用程序`-`Windows 版本`为`Windows 11`，`显示`-`屏幕分辨率`调大以适应本机分辨率。

![](assets/20250309231350.png =300x)
![](assets/20250309231516.png =300x)

选择下载的安装包，点击`运行程序`安装，安装前会提示先安装 mono。

![](assets/20250309231054.png)

安装后会在启动器创建快捷方式但打不开。

修改 Wine 运行器中执行程序为`/home/duanluan/.wine/drive_c/Program Files/PremiumSoft/Navicat Premium 17/navicat.exe`，名称随便，创建快捷方式到桌面，参考这个内容修改启动器中现有快捷方式的内容。

![](assets/20250310001055.png)

```shell
$ vim ~/.local/share/applications/wine/Programs/PremiumSoft/Navicat\ Premium\ 17.desktop

[Desktop Entry]
Name=Navicat Premium 17
Exec=env WINEPREFIX='/home/duanluan/.wine' WINEDEBUG=FIXME,ERR,WARN,TRACE,Message  /home/duanluan/.deepwinerunner/wine/wine-staging-wow64-10.2-debian10-amd64/bin/wine '/home/duanluan/.wine/drive_c/Program Files/PremiumSoft/Navicat Premium 17/navicat.exe'  
Icon=D66E_navicat.0
Type=Application
StartupNotify=true
```
