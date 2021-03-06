+++
categories = ["开发", "中文"]
date = "2016-04-27T05:46:16Z"
tags = ["Linux", "Ubuntu", "Atom"]
title = "在瘟到死石中使用 Linux 进行开发"

+++

简述
------

开发 Node, Ruby, PHP 等技术的时候，总是面临 Windows 问题，不是说他们不支持 Windows，其实要装是可以装的。但是他们的生态运行在 Windows 上时，某些组件的运行结果可能会改变，或出现运行不稳定的情况。通常程序猿，尤其是老美的程序猿更倾向用 Mac 或 Linux 搞开发。搞 Web 的更是如此，工程师都希望开发环境和生产环境尽可能相近，减少不必要的 Bug，服务器是 Linux 最好生产环境也是 Linux，最少也要支持 posix 规范。于是乎，虽然 Windows 的市场份额不小，可是开源社区反而是对 Linux 版本和 Mac 版本的软件支持更为出色。我用 Linux 有段时间了，不过如果非要我在硬盘里分个区单独装 Linux，会显得略繁琐。娱乐软件的支持和硬件驱动的支持一度搞得我焦头烂额。我的电脑几乎不关机，休眠就够了，所以重启切换系统这项工作太反人类了233。既然这个东西已经不是一个 Geek 的玩具，反倒是吃饭和学习的家伙了。易于配置，易于启动，易于恢复，这三项标准就显得尤为重要。虚拟机的整机快照功能，可以非常方便的做到这一点，我也不用虚拟机玩游戏，性能损失也可以忽略不计。

结论
------

> Update: 知名 YouTube 主播 [quidsup](https://www.youtube.com/user/quidsup) 一直在安利 Ubuntu Mate/Linux Mint……Unity 貌似吃内存和显存很多。我尝试了一下。虽然 Ubuntu Unity 确实很漂亮，但是感觉基于 Gnome3 的 Cinnamon 更省资源，更流畅，也更传统（毕竟基于Gnome）。（纯主观感受，毫无科学依据）不过呢，我已经折腾很久的 Ubuntu 了。感觉还是不需要再折腾下去了。Popularity is my first concern.

先说结论，目前我的选择是免费版 `VMware Workstation Player 12`(非商业用途使用) 加 `Ubuntu 16.04 LTS`。目前 Ubuntu 还是有些小毛病。但是正常开发上网看片都没问题。


FAQs
------

### 为毛用虚拟机

大多数的娱乐和工作工具还是必须用 Windows 的（尤其是中文环境）且不想折腾 Wine<br>完~


### 作为早期 Deepin 用户为毛不支持 Deepin

1. Deepin 在新加坡软件更新巨慢啊……不仅源的数量多，而且最近的镜像在印尼。每次 `apt-get update` 都等得我想死啊。用了 Ubuntu 之后，5~6 个源，下载速度也有提高毕竟来自星国大的镜像站就在本地。
2. Deepin 在 VirtualBox 里卡得一逼。Ubuntu 在 virtualBox 比 Deepin 强多了。它本身不建议使用虚拟机环境也是有道理的。（我依然推荐VMware）
3. 稳定压倒一切（此处仅指软件）

> Update: Linux Mint 的东南亚镜像源也在印尼/菲律宾。但是下载速度飞快。原因不明，难道是他们自己定制了更新器的下载模块？
 

### 为毛不用 VirtualBox

~~我用过，可是你知道你最大只能给你的 VM 加 128M 的显存么？！！！！我一开始以为 Linux 不吃显存，可是 tm 动不动就卡啊， Deepin是直接死机，Ubuntu是死一会儿好一会儿，而且驱动貌似也有问题。
当，VMware 里分配给虚拟机的显存数量默认为 `768M`。你就会看到屏幕所有的动画几乎都毫无卡顿，几乎媲美原生系统。相信我，你绝对再也回不去了！！！只要我接到新的赚外快机会，我就买商业版！真的，太爽了！软件的稳定就是安心！可能 VirtualBox 有些 `CLI  API` 可以做到这些吧，可是为毛要折腾呢？
稳定压倒一切~~
128M 只是2D视频的显存。128已经够用了。而用于3D的显存是无限的，显卡上有多少就可以用多少。
至于为什么会卡，我还是不太清楚。如果我将来可以换一个SSD作为主力硬盘的话，我的确很有可能会转回去使用 `VirtualBox`。


### 用什么做开发

最近都在玩前端，前端比后端酷炫好玩而且环境配置更简单。
我的学习历程基本都在《Frontend Learning Note》里介绍的差不多了。
我用这些东西：

- Zsh：加git, ssh-agent插件 (See more @ https://github.com/qiansen1386/vagrant-frontend/blob/master/zsh.install.sh)
- VIM/gedit: 我是用 DigitalOcean 的时候，看他们的官方教程学得 Vim，感觉挺好用的，反而不习惯 nano 这种功能用选项的笔记本工具了。gedit 嘛就是用 GUI 界面的时候用。
- Atom: (See more @ https://github.com/qiansen1386/frontend-dev-vue#suggested-atom-plugins)
- Google-Chrome-stable: 谷歌大法好！ (看这里 @ [ECMAScript compatibility table](https://kangax.github.io/compat-table/es6/)) 另外也是我主要的插件和收藏都在谷歌服务里。
- [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) 1. Firefox 一般比 Google 更尊重标准。2. Linux 下 比 Google Chrome 启动更快，吃资源更少，安装也更方便。然而，我需要安装 Developer Edition，多了一个步骤。
- [Node Version Manager](https://github.com/creationix/nvm): `nvm` 我一般都是必装的。


> 注1：如果出现 `sudo node`，或者 `sudo npm` 时，出现 `Command Not Found` 错误。建议执行以下代码，把 node 复制一份到 `usr`。
详见 @ [Can't use NVM from root (or sudo)](http://stackoverflow.com/questions/21215059/cant-use-nvm-from-root-or-sudo) & [How To Install Node.js with NVM (Node Version Manager) on a VPS - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-with-nvm-node-version-manager-on-a-vps#-installing-nodejs-on-a-vps)
```shell
n=$(which node);n=${n%/bin/node}; chmod -R 755 $n/bin/*; sudo cp -r $n/{bin,lib,share} /usr/local
```

> 注2: 安装 Firefox Developer Edition 的最简方法：
```shell
sudo add-apt-repository ppa:ubuntu-mozilla-daily/firefox-aurora
sudo apt-get update
sudo apt-get install firefox
```
详见 @ [How do I install the Firefox Developer Edition? - AskUbuntu](http://askubuntu.com/questions/548003/how-do-i-install-the-firefox-developer-edition)


### 推荐配置

类目|说明
-----|-------------------
处理器|分配等效 4 逻辑核
内存|`6~8G`，亲测，如果只分配`4G`，用 `Atom` 和 `Chrome` 会卡
硬盘|我放了`300G`，放心地往大了放就好了，这不是实际使用空间，只是最大使用空间。
显存|`1G`吧
打印机|要手动删除虚拟打印机，不为什么，反正用不到，看着烦
驱动|不需要特殊驱动，但是VMware Tools一定要装，跟VirtualBox extension pack是一个意思


### 安装注意事项

配置好硬件之后，就可以安装了。VMware 在装 ubuntu 的时候，并不用真正的走流程安装的（手动装当然也可以）。
它问一些基本信息，然后用一个私有方案复制文件，就可以直接“简易安装”，不是很懂。我默认安装下来。跟自己装没啥区别。
折腾输入法的时候有些麻烦，但是没有什么好总结的，莫名其妙就坏了，莫名其妙就好了。

1. 千万别乱装软件源。如果出错了就取消掉。平时没事的时候很多第三方源我都取消掉了。速度上有提升，软件更新的过程也不容易出错。当然，你没法用最新的软件了。我的想法是什么时候想更新了，什么时候再勾选上他们。（可能有问题）
2. Ubuntu Software 软件进行安装和卸载很容易出错的，用 `synaptic` 更好些。
3. 安装完 `Fcitx` 和 `sogou` 之后，不要手贱卸载 `ibus`。这货跟很多 unity 组件有依赖，卸载他，ubuntu desktop的组件们也会跟着消失。（这种情况下，重装 `ibus` 可能管用；如果不管用，则需要把当前的 `.compiz-1` 文件夹改名为 `.compiz-1.old` 之类的。重置默认设置。之后备份出来的的 `.compiz-1` 文件夹就可以删掉了。）
4. Linux 锁定状态下，是否可以通过 Chrome remote Desktop访问，我目前不太清楚。但是访问锁定状态下的 Windows 里的虚拟机里的锁定状态下的 Linux 里的 `Chrome RDP` 就实在是做不到了，需要穿过太多层了。任何一层阻隔了访问权限也会出问题，而且搞不好就会暴露很多安全隐患不建议这么做，最好用共享网盘分享文件，而非共享访问权限。

> 官方自带的 Backup 组件，在安装 `Chrome RDP` 之后会出现异常反应，如无休止地占用海量内存（症状类似内存泄漏）。建议不要安装 Google RDP，尚不知道 TeamViewer 等其他`VNC`软件是否有类似 Bug。

### 本土化 与 个性化

1. Fctix => Sogou 拼音（必须）
2. WPS (中文字体)（可选）
3. 思源黑体（自带 Noto 的版本）
4. 有道词典（没有快捷键呼出，没有用户登录，略鸡肋）
5. 一个扁平化的黑色系主题！嘿嘿嘿。

> 喂丸·待续
<div class="thumbinner" style="width:222px;">
<svg xmlns="http://www.w3.org/2000/svg" id="svg2" viewBox="0 0 200 200">
  <g id="glass" fill="none" stroke="#000">
    <path stroke-width="10" d="M31.625 53h46.5v33h-46.5z"/>
    <path stroke-width="10" d="M121.625 53h46.5v33h-46.5z"/>
    <path stroke-width="9" d="M80.375 70.014h37"/>
  </g>
  <g id="..">
    <path d="M82.72 128.695q-3.96 0-6.48-2.52-2.52-2.7-2.52-6.48 0-3.78 2.52-6.3 2.52-2.7 6.48-2.7 3.78 0 6.3 2.7 2.52 2.52 2.52 6.3t-2.52 6.48q-2.52 2.52-6.3 2.52z"/>
    <path d="M117.28 128.695q-3.78 0-6.3-2.52-2.52-2.7-2.52-6.48 0-3.78 2.52-6.3 2.52-2.7 6.3-2.7 3.96 0 6.48 2.7 2.52 2.52 2.52 6.3t-2.52 6.48q-2.52 2.52-6.48 2.52z"/>
  </g>
  <g id="naive" fill-opacity=".2">
    <path d="M-96.22 146.875h12.24l1.26 12.6h.54q6.3-6.3 13.14-10.44 7.02-4.32 16.2-4.32 13.86 0 20.16 8.64 6.48 8.64 6.48 25.56v55.44h-14.76v-53.46q0-12.42-3.96-17.82-3.96-5.58-12.6-5.58-6.84 0-12.06 3.42-5.22 3.42-11.88 10.08v63.36h-14.76v-87.48z"/>
    <path d="M22.38 236.515q-10.98 0-18.36-6.48-7.2-6.48-7.2-18.36 0-14.4 12.78-21.96 12.78-7.74 40.86-10.8 0-4.14-.9-8.1-.72-3.96-2.7-7.02-1.98-3.06-5.58-4.86-3.42-1.98-8.82-1.98-7.56 0-14.22 2.88-6.66 2.88-11.88 6.48L.6 156.055q6.12-3.96 14.94-7.56 8.82-3.78 19.44-3.78 16.02 0 23.22 9.9 7.2 9.72 7.2 26.1v53.64H53.16l-1.26-10.44h-.54q-6.3 5.22-13.5 9-7.2 3.6-15.48 3.6zm4.32-11.88q6.3 0 11.88-2.88 5.58-3.06 11.88-8.82v-24.3q-10.98 1.44-18.54 3.42-7.38 1.98-12.06 4.68-4.5 2.7-6.66 6.3-1.98 3.42-1.98 7.56 0 7.56 4.5 10.8 4.5 3.24 10.98 3.24z"/>
    <path d="M92.922 146.875h14.76v87.48h-14.76v-87.48z"/>
    <path d="M124.62 146.875h15.3l16.56 49.68 3.96 12.96q2.16 6.48 4.14 12.78h.72q1.98-6.3 3.96-12.78l3.96-12.96 16.56-49.68h14.58l-30.96 87.48h-17.28l-31.5-87.48z"/>
    <path d="M256 236.515q-8.82 0-16.56-3.06-7.56-3.24-13.32-9-5.58-5.94-8.82-14.4t-3.24-19.26q0-10.8 3.24-19.26 3.42-8.64 8.82-14.58 5.58-5.94 12.6-9 7.02-3.24 14.58-3.24 8.28 0 14.76 2.88 6.66 2.88 10.98 8.28 4.5 5.4 6.84 12.96 2.34 7.56 2.34 16.92 0 2.34-.18 4.68 0 2.16-.36 3.78h-59.04q.9 14.04 8.64 22.32 7.92 8.1 20.52 8.1 6.3 0 11.52-1.8 5.4-1.98 10.26-5.04l5.22 9.72q-5.76 3.6-12.78 6.3-7.02 2.7-16.02 2.7zm19.26-52.92q0-13.32-5.76-20.16-5.58-7.02-15.84-7.02-4.68 0-9 1.8-4.14 1.8-7.56 5.4-3.42 3.42-5.76 8.46-2.16 5.04-2.88 11.52h46.8z"/>
  </g>
</svg>
</div>