---
title: Ubuntu20.04初步配置教程
top: false
cover: false
toc: true
date: 2021-05-08 10:56:03
author: bucaike
img: https://i.loli.net/2021/05/08/DcP4pRvWausHMCl.jpg
coverImg: https://i.loli.net/2021/05/08/DcP4pRvWausHMCl.jpg
mathjax: false
tags:
  - Linux
  - 优化
categories:
  - 技术 
---

> 本文主要介绍下`Ubuntu20.04`在我手上的日常使用，以及一些一本软件的安装，作为大家的参考。
>
> 我的环境：
>
> ```bash
> black@black-OMEN:~$ neofetch 
>             .-/+oossssoo+/-.               black@black-OMEN 
>         `:+ssssssssssssssssss+:`           ---------------- 
>       -+ssssssssssssssssssyyssss+-         OS: Ubuntu 20.04 LTS x86_64 
>     .ossssssssssssssssssdMMMNysssso.       Host: OMEN by HP Laptop 
>    /ssssssssssshdmmNNmmyNMMMMhssssss/      Kernel: 5.4.0-40-generic 
>   +ssssssssshmydMMMMMMMNddddyssssssss+     Uptime: 46 mins 
>  /sssssssshNMMMyhhyyyyhmNMMMNhssssssss/    Packages: 1922 (dpkg), 11 (s 
> .ssssssssdMMMNhsssssssssshNMMMdssssssss.   Shell: bash 5.0.16 
> +sssshhhyNMMNyssssssssssssyNMMMysssssss+   Resolution: 1920x1080 
> ossyNMMMNyMMhsssssssssssssshmmmhssssssso   DE: GNOME 
> ossyNMMMNyMMhsssssssssssssshmmmhssssssso   WM: Mutter 
> +sssshhhyNMMNyssssssssssssyNMMMysssssss+   WM Theme: Yaru-dark 
> .ssssssssdMMMNhsssssssssshNMMMdssssssss.   Theme: Yaru-dark [GTK2/3] 
>  /sssssssshNMMMyhhyyyyhdNMMMNhssssssss/    Icons: Yaru [GTK2/3] 
>   +sssssssssdmydMMMMMMMMddddyssssssss+     Terminal: gnome-terminal 
>    /ssssssssssshdmNNNNmyNMMMMhssssss/      CPU: Intel i5-7300HQ (4) @ 3 
>     .ossssssssssssssssssdMMMNysssso.       GPU: Intel HD Graphics 630 
>       -+sssssssssssssssssyyyssss+-         GPU: NVIDIA GeForce GTX 1050 
>         `:+ssssssssssssssssss+:`           Memory: 2699MiB / 11867MiB 
>             .-/+oossssoo+/-.
>                                                                    
>                                                                    
> ```

## 基本设置

### 终端

> 参考：[A random emoji in your terminal prompt. How and Why!](https://loige.co/random-emoji-in-your-prompt-how-and-why/)
>
> 参考：[[Mac 终端窗口配置](https://www.cnblogs.com/himonkey/p/11853487.html)](https://www.cnblogs.com/himonkey/p/11853487.html#%E5%AE%89%E8%A3%85%E5%AD%97%E4%BD%93)

​	展示下我的终端：

![我的终端界面](https://i.loli.net/2021/05/08/sFyWmPgZ65T2Oic.png)

#### 展示命令成功与否

命令执行得正确与否会有不同的表现。编辑代码`~/.bashrc`直接添加下面的代码：

```bash
function success_indicator() {
    if [ $? -eq 0 ] ; then
        echo "😎"
    else
        echo "💩"
    fi
}
export PS1="\$(success_indicator)\[\e[32;40m\]\u\[\e[m\]\[\e[32m\]@\[\e[m\]\[\e[32m\]\h\[\e[m\]:\[\e[34m\]\W\[\e[m\]👉 "
```

​	这里还使用了两个工具：[.bashrc PS1 generator by Julien Ricard](http://bashrcgenerator.com/) 和 [Easy Bash PS1 Generator by Josh Matthews](http://ezprompt.net/)

#### 展示文件夹和文件信息

* 安装字体

  原有的字体是不能显示这么多字符的。去[nerdfonts](https://www.nerdfonts.com/font-downloads)下载，我下载的是**Hack Nerd Font**。安装就行，没必要全部安装。

  终端里面设置字体。

* 安装`clolorls`

  首先需要安装`ruby`等。

  ```bash
  sudo apt install ruby ruby-dev
  ```

  然后：

  ```bash
  sudo gem install colorls
  ```

* 设置别名

  `vim ~/.bashrc`添加下面两行：

  ```bash
  alias ll='colorls -lA --sd --gs --group-directories-first'
  alias ls='colorls --group-directories-first'
  ```

  

### 耳机杂音解决（Realtek ALC295）

​	这个问题困扰了我好久了，之前装过`kali`，也出现了这样的情况，当时以为是通病，后来发现原来只有我有此问题。所以说，如果你的声音也出现了问题，可以搜索下自己的声卡型号。

​	终端输入：`sudo alsamixer`，回车，可以看到下面的信息：

![](https://i.loli.net/2020/07/21/eyqwDLd5obJCrSf.png)

​	其中的`Chip`即是你的声卡型号。

​	我在[这个网站](https://bugs.launchpad.net/ubuntu/+source/alsa-driver/+bug/1648183)找到了解决办法。首先安装`alsa-tools`：

```bash
sudo apt install alsa-tools
```

然后，在`/usr/local/bin`下写个脚本：

```bash
#! /bin/bash
hda-verb /dev/snd/hwC0D0 0x20 SET_COEF_INDEX 0x67
hda-verb /dev/snd/hwC0D0 0x20 SET_PROC_COEF 0x3000
```

并加权。运行之后即时生效。

> **UPDATE: **此问题官方已修复。



### 设置文件夹为英文

​	刚装好的系统，如果你设置的语言是中文，那么其在家目录下面的文件夹名称全部都是中文，而我们经常要在终端里面进行切换文件夹等操作，有中文非常不方便，所以这一项是我必操作的步骤。

​	网上比较流行的一种方法是先将环境切换成英文，然后再切换成中文。特别麻烦，还要重启，也违背了`Linux`一切皆文件的思想，不知道这种方法怎么流行起来的。下面介绍我的方法

* 编辑文件`user-dirs.dirs`

  ```bash
  black@black-OMEN:~$ vim ~/.config/user-dirs.dirs
  ```

  更改为：

  ![](https://i.loli.net/2020/07/21/UxTCVolPB6DbuA7.png)

> vim的安装用法可参照我的另一篇文章：[我打开新Linux系统的方式](http://bucaike.top/2020/05/29/%e6%88%91%e6%89%93%e5%bc%80%e6%96%b0linux%e7%b3%bb%e7%bb%9f%e7%9a%84%e6%96%b9%e5%bc%8f/)
>
> vim的配置文件`.vimrc`我推荐是自己备份一下，然后需要的时候直接拷贝过去就行。

此时，此时再直接修改文件夹名称，可以看到文件夹有对应的图标了，这说明映射关系是正确的：

![](https://i.loli.net/2020/07/21/ZXc2kwJRuvxY7iE.png)

### 设置账号并同步日历等

> 这个我个人认为很重要，我的日历上面有我的各种日程，各种终端上面，只要登陆了我这个账号，那么日程消息就会同步过去，不会错过重要的日子和人。
>
> 我用的是微软的账户，其他终端如安卓，ios 上面都比较简单，但是`Linux`上面比较麻烦一点。

* Microsoft 应用密码

  这一步应该不是必须的，但是我建议你做一下。点击此[链接](https://account.live.com/proofs/AppPassword)，得到应用密码。

  如果你没有，那么可以从[微软账户](https://account.microsoft.com/)转到“安全性”顶部菜单），更多安全性选项，“创建”新的应用程序密码（页面中间）。

  如果你不能创建，那么是因为你没有设置“双重验证”，关于如何设置双重验证，微软已经给了文档，所以不再赘述。

* Evolution&Evolution-ews

  > 这里是比较关键的一步。对于Linux用户而言，将Outlook.com日历与Gnome Shell（Gnome 3）结合使用几乎是不可能的任务，这是由于用于与Microsoft通信的EAS（Exchange Active Sync）协议所致。
  >
  > 现在，使用EWS（Exchange Web服务），将Outlook.com日历（还包括邮件和联系人）集成到Gnome Shell中，很简单，只需一个扩展即可。

  我们需要安装Evolution（MS Outlook的Linux替代产品）和Evolution-ews扩展。

  ```bash
  sudo apt install Evolution Evolution-ews
  ```

* 登陆账户

  打开“设置” ，“在线账户”，添加账号，**选Microsoft Exchange**（而不是“微软”）。

  在这里，电子邮箱输入你的的电子邮件地址，密码填刚才的 Microsoft 应用密码，展开“自定义”区域，再次输入您的电子邮件地址**（与上面相同）作为用户名**，重要的是输入Outlook.office365.com 作为服务器。然后点击“连接”。

  ![](https://i.loli.net/2020/07/21/V5pl3xvtk2Omnf7.png)

* 设置同步

  现在可以点击你已登录的账户然后选择同步项了：

  ![](https://i.loli.net/2020/07/21/4FuC3gKqiLlzOZs.png)

### 动态壁纸（24h）

> ​	这里的动态壁纸，是指的像`MacOS`里面的`24h`动态壁纸，壁纸会随着时间的推移而有不同的表现。如果想要将壁纸设置为动画，可以参考下节。

[参考](https://technastic.com/macos-mojave-dynamic-wallpaper-on-linux/)

* 下载`macOS Mojave`壁纸

  下载地址：[**mojave_dynamic.zip**](https://files.rb.gd/mojave_dynamic.zip)

  将压缩包里面的内容提取到`~/Pictures/wallpapers`里，然后将文件夹重命名为**mojave-background**。最后的文件路径将会是：

  ```bash
  /home/black/Pictures/wallpapers/mojave-background/
  ├── __MACOSX
  ├── mojave_dynamic_10.jpeg
  ├── mojave_dynamic_11.jpeg
  ├── mojave_dynamic_12.jpeg
  ├── mojave_dynamic_13.jpeg
  ├── mojave_dynamic_14.jpeg
  ├── mojave_dynamic_15.jpeg
  ├── mojave_dynamic_16.jpeg
  ├── mojave_dynamic_1.jpeg
  ├── mojave_dynamic_2.jpeg
  ├── mojave_dynamic_3.jpeg
  ├── mojave_dynamic_4.jpeg
  ├── mojave_dynamic_5.jpeg
  ├── mojave_dynamic_6.jpeg
  ├── mojave_dynamic_7.jpeg
  ├── mojave_dynamic_8.jpeg
  └── mojave_dynamic_9.jpeg
  
  1 directory, 16 files
  ```

* 获取XML脚本

  下载地址：[**mojave.xml**](https://gist.githubusercontent.com/trongthanh/7d632e90687e1bc219e1f3262d337702/raw/8659a5432ad1ace0de3c8062435400db8a68f1cf/mojave.xml)

  在您可以使用脚本之前，您需要在此处进行一些更改。在您选择的文本编辑器中打开xml文件。然后在脚本中查找并用你自己的用户名替换文件中的 **thanh**。例如，我在系统上使用的用户名是**balck**，因此会将文件中每一个**thanh**替换成**black**，完成后，保存。

* 设置`macOS Mojave`动态壁纸

  1. 安装`gnome-tweak-tools`

     ```bash
     sudo apt install gnome-tweak-tools
     ```

  2. 终端运行`gnome-tweaks`，在外观中选择xml文件作为壁纸：

     ![](https://i.loli.net/2020/07/21/5e2aXkIHi7Gzb4Y.png)

## 安装基本软件

### 备份软件`TimeShift`

​	阻止人们使用`Linux`系统的一个大原因我觉得是怕搞坏，即使在使用了`Linux`系统几年的我身上也是比较怕，所以，我们需要有良好的备份习惯。

​	`TimeShift`这个软件支持GUI，对新手很友好，也支持**增量备份**。下面是这个软件的介绍信息：

> DESCRIPTION
>        timeshift  is a system restore utility which takes snapshots of
>        the system at regular intervals. These  snapshots  can  be  re‐
>        stored  at  a later date to undo system changes. Creates incre‐
>        mental snapshots using rsync or  BTRFS  snapshots  using  BTRFS
>        tools.

* 安装

  ```bash
  sudo apt update && sudo apt install timeshift
  ```

  之后我们就可以在菜单看到软件了。

* 使用

  打开软件，会有个使用向导，按照步骤走就行。在用户主目录这里，我建议是**Include All Files**。然后就可以开始第一次备份。要注意的是，由于是第增量备份，所以第一次备份时的时间会比较长，以后的每次备份，只会在原有的基础上修改改动的部分。

  点击创建，会自动备份，备份完了大概是这样（我分配的空间较少，所以禁用了自动备份）：

  ![](https://i.loli.net/2020/07/21/vlG7eTEWzVu1RNa.png)

## 安装deepin-win，QQ，WeChat

> 国民应用，没办法，不得不装，deepin在这方面走在了前面，有人将deepin-wine移植到了Ubuntu上，项目地址：
>
> [github](https://github.com/wszqkzqk/deepin-wine-ubuntu)
>
> [gitee](https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu)

* 安装`deepin-wine`

  ```bash
  git clone https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu.git && cd deepin-wine-for-ubuntu
  ```

  选择合适于你的安装脚本，加可运行权限，我这里选择的是`install_2.8.22.sh`，执行：

  ```bash
  sudo chmod +x install_2.8.22.sh && sudo ./install_2.8.22.sh
  ```

* 安装软件

  下载并安装所需要的`deepin-wine`容器 *（建议在终端下使用`dpkg -i`安装容器，否则容易误报依赖错误）*

  * 可使用`deepin`发布的最新版容器安装包：

    1. [QQ](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/)

    2. [TIM](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.office/)
    3. [QQ轻聊版](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im.light/)

    4. [微信](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/) 如果出现依赖错误，请下载[这个版本](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.wechat_2.6.8.65deepin0_i386.deb)
    5. [Foxmail](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.foxmail/)

    6. [百度网盘](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.baidu.pan/)

    7. [360压缩](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.cn.360.yasuo/)

    8. [WinRAR](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.cn.com.winrar/)

    9. [迅雷极速版](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.thunderspeed/)

    10. [千牛卖家工作台](https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.taobao.aliclient.qianniu/)

    其它deepin-wine容器：[阿里云镜像下载](https://mirrors.aliyun.com/deepin/pool/non-free/d/)

  * 若版本不兼容，可选择下载安装以下旧版包文件：

    1. [QQ](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.qq.im_9.1.8deepin0_i386.deb)

    2. [TIM](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.qq.office_2.0.0deepin4_i386.deb)

    3. [QQ轻聊版](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.qq.im.light_7.9.14308deepin8_i386.deb)

    4. [微信](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.wechat_2.6.8.65deepin0_i386.deb)

    5. [Foxmail](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.foxmail_7.2deepin3_i386.deb)

    6. [百度网盘](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.baidu.pan_5.7.3deepin0_i386.deb)

    7. [360压缩](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.cn.360.yasuo_4.0.0.1060deepin3_i386.deb)

    8. [WinRAR](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.cn.com.winrar_5.3.0deepin2_i386.deb)

    9. [迅雷极速版](https://gitee.com/wszqkzqk/deepin-wine-containers-for-ubuntu/raw/master/deepin.com.thunderspeed_7.10.35.366deepin18_i386.deb)

* 手动更改配置（winecfg）

  执行 `WINEPREFIX=~/.deepinwine/容器名称 deepin-wine winecfg` 即可，也可以用此方法来调整缩放问题

* 解决系统非中文语言环境时软件无法设置为中文

  在/opt/deepinwine/tools/run.sh 中将 WINE_CMD 那一行修改为 WINE_CMD="LC_ALL=zh_CN.UTF-8 deepin-wine"

* 微信更新问题

  如果出现微信提示跟新问题执行这一条语句即可

  ```bash
   wget -qO- https://deepin-wine.i-m.dev/setup.sh | sudo sh
  ```

* [wine 应用程序全局快捷键无效的解决方案](https://blog.diqigan.cn/posts/wine-global-hotkey-problem.html)

  1. 安装 xdotool

     直接在命令行运行以下命令即可:

     ```bash
     sudo apt install --no-install-recommends xdotool
     ```

  2. 编写 xdotool 脚本

     > 思路: Wine 应用在后台无法接收到快捷键状态, 此时借助 xdotool 向 Wine 应用发送模拟按键信息即可.

     在合适的位置新建一个脚本文件 "open_wechat.sh", 写入以下内容:

     ```
     #!/bin/sh
     #在当前运行的应用中找到名为WeChat.exe的应用程序，并向它发送按键事件"ctrl+alt+W"
     #WeChat的可执行文件名为WeChat.exe，如果是其它应用程序就修改成其它应用程序的可执行文件名, 应用名称大小写敏感, 一个字母都不能错!
     xdotool key --window $(xdotool search --limit 1 --all --pid $(pgrep WeChat.exe)) "ctrl+alt+W"
     ```

     赋予脚本可执行权限:

     ```
     chmod +x open_wechat.sh
     ```

     如果此时你的微信正好运行在后台, 执行这个脚本就可以把它召唤到前台. 如果没有, 请检查脚本是否有错误。

  3. 设置快捷键

     图形界面依次打开 "设置" -> "设备" -> "键盘", 点击列表最底部的 "+" 号添加自定义快捷键.

     [![快捷键设置](https://camo.githubusercontent.com/23ae69e9c1369dcc18325a989469b499dcf36f64/68747470733a2f2f696d616765732e67697465652e636f6d2f75706c6f6164732f696d616765732f323032302f303131372f3037353134315f34643137666162345f313434323533302e706e67)](https://camo.githubusercontent.com/23ae69e9c1369dcc18325a989469b499dcf36f64/68747470733a2f2f696d616765732e67697465652e636f6d2f75706c6f6164732f696d616765732f323032302f303131372f3037353134315f34643137666162345f313434323533302e706e67)

     * 名称随便, 填写 "打开微信" 即可;

     - 命令填写刚才编写的脚本的**全路径**;
     - 快捷键设置自己想用的快捷键即可, 建议于应用内部快捷键相同;
     - 最后点击"添加"即可.

* 问题记录

  1. 微信无法发送图片

     ```bash
     sudo apt-get install libjpeg62:i386
     ```
     
  2. Fcitx（常见的就是搜狗）不能输入：
  
     1. 找到wineQQ的安装目录，我的是在：`/opt/deepinwine/apps/Deepin-QQ`下，有个`run.sh`，vim编辑，最后一行添加：
  
        ```bash
        #=================================
        #搜狗输入法输入中文的问题
        export XMODIFIERS="@im=fcitx"
        export GTK_IM_MODULE="fcitx"
        export QT_IM_MODULE="fcitx"
        ```
  
     2. 如果是`Gnome`平台，可能会出现最小化之后不能再次输入的情况，还需要输入：
  
        ```bash
        gsettings set org.gnome.settings-daemon.plugins.keyboard active false 
        ```
  
        在`/etc/envirment`下添加：
        
        ```bash
        export XMODIFIERS="@im=fcitx"
        export GTK_IM_MODULE="fcitx"
        export QT_IM_MODULE="fcitx"
        ```
        
        同时也在`/.profile`下加入。

## 更改键盘映射

这里介绍一般方法，并举出一个例子。

1. 找到你需要改键的`ketcode`

   输入命令`xev`，就能捕捉到一切动作，从中找出`keycode`

2. 导出目前使用的键盘映射

   ```bash
   xmodmap -pke > ~/.Xmodmap
   ```

3. 修改文件

   我将键盘上的大小写键改成了方向键→，于是编辑文件，首行加上

   ```bash
   clear Lock
   ```

   把`keycode  66`改成`keycode  66 = Right NoSymbol Right`

   结尾上：

   ```bash
   add Lock = Caps_Lock
   ```

4. 生效

   ```bash
   xmodmap ~/.Xmodmap
   ```

5. 自动激活

   编辑`~/.xinitrc`

## zip解压乱码

### unzip解决方案：

```bash
unzip -O cp936 ./1.zip
```



## zsh

### 安装zsh的包管理器`antigen`

```bash
curl -L git.io/antigen > .antigen.zsh
```

### 配置

```bash
vim .zshrc
# 写入
source /home/black/Tools/antigen.zsh

# 加载oh-my-zsh库
antigen use oh-my-zsh

# 加载原版oh-my-zsh中的功能(robbyrussell's oh-my-zsh).
antigen bundle git
antigen bundle heroku
antigen bundle pip
antigen bundle lein
antigen bundle command-not-found

# 语法高亮功能
antigen bundle zsh-users/zsh-syntax-highlighting

# 代码提示功能
antigen bundle zsh-users/zsh-autosuggestions

# 自动补全功能
antigen bundle zsh-users/zsh-completions

# 加载主题
#antigen theme robbyrussell
antigen theme romkatv/powerlevel10k

# 保存更改
antigen apply

```

## 使用别名alias

1. 确保`.bashrc`中有这一段：

   ```bash
   # Alias definitions.
   # You may want to put all your additions into a separate file like
   # ~/.bash_aliases, instead of adding them here directly.
   # See /usr/share/doc/bash-doc/examples in the bash-doc package.
   
   if [ -f ~/.bash_aliases ]; then
       . ~/.bash_aliases
   fi
   ```

2. 编辑`~/.bash_aliases`

   > 没有就自己创建

   比如：写上

   ```bash
   alias nvrun="__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia"
   ```

3. 检查成功

> 如果你是使用的是Zsh，那么将第一步的代码添加到`.zshrc`里面，然后执行后面的步骤。

## 启动时自动使用独显

> 添加别名已经讲过了

1. 添加别名

   ```bash
   alias nvrun="__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia"
   ```

2. 使用

   ```bash
   nvrun steam
   ```

   

## steam play 玩游戏时使用独显

游戏启动项加上`WINEDLLOVERRIDES="dxgi=n" %command%`这句

