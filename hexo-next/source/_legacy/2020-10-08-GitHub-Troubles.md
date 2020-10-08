---
title: Git+GitHub, Trouble Solver
date: 2020-10-08 22:59:35
updated: 2020-10-08 22:59:35
categories:
  - Records
tags:
  - Git
  - Debug
mathjax: false
---



# 网络问题

## Failed to connect port 443: Timed out

系统环境: Win 10 (not really matter)

出现问题
```bash
λ git push
fatal: unable to access 'https://github.com/eustomaqua/repo.git/': Failed to connect to github.com port 443: Timed out
```

**Attempt 1.**  

查询解决方法 (失败)
```bash
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
```

这种代理设置的方法我开始设置的是 local ，发现无效后取消了再设置 global ，仍然无效。所提示的错误信息为
```bash
λ git push --set-upstream origin ver3b
fatal: unable to access 'https://github.com/eustomaqua/repo.git/': Failed to connect to 127.0.0.1 port 1080: Connection refused
```

其实我第一次设置时因为疏漏只设置了 local 的 http.proxy ，会提示一样的错误信息；同时设置 local 的 https.proxy 也不会让情况变得更好点。
然后我尝试了直接设置 global 的两个代理，依旧无效。

备注，取消设置代理的方法为
```bash
git config --local --unset http.proxy
git config --local --unset https.proxy
```

**Attempt 2.**

ref: [GitHub无法访问、443 Operation timed out的解决办法](https://juejin.im/post/6844904193170341896)

- Step 1. 打开 [https://github.com.ipaddress.com/](https://github.com.ipaddress.com/) 记录 **1** 个 IP 地址
  参考图 ref
  <img src="https://user-gold-cdn.xitu.io/2020/6/17/172bde579dbb3de8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" width="87%">
- Step 2. 打开 [https://fastly.net.ipaddress.com/github.global.ssl.fastly.net#ipinfo](https://fastly.net.ipaddress.com/github.global.ssl.fastly.net#ipinfo) 记录 **1** 个 IP 地址
  参考图 ref
  <img src="https://user-gold-cdn.xitu.io/2020/6/17/172bde57a05985dd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" width="87%">
- Step 3. 打开 [https://github.com.ipaddress.com/assets-cdn.github.com](https://github.com.ipaddress.com/assets-cdn.github.com) 记录 **4** 个 IP 地址
  参考图 ref
  <img src="https://user-gold-cdn.xitu.io/2020/6/17/172bde57a0a40370?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" width="87%">

- Step 4. 打开电脑的 hosts 文件，添加如下命令，然后保存即可
  ```bash
  140.82.113.3(IP Address of Pic 1) github.com
  199.232.69.194(IP Address of Pic 2) github.global.ssl.fastly.net
  185.199.108.153(IP Address of Pic 3) assets-cdn.github.com
  185.199.109.153(IP Address of Pic 3) assets-cdn.github.com
  185.199.110.153(IP Address of Pic 3) assets-cdn.github.com
  185.199.111.153(IP Address of Pic 3) assets-cdn.github.com
  ```
- Step 5. 在终端用命令刷新 DNS 缓存

Windows
- Step 4. 快速打开 hosts 文件位置
  - (1) 使用 Win+R 组合快捷键打开运行命令框，然后键入 Hosts 文件路径，即 `C:\WINDOWS\system32\drivers\etc`
  - (2) 从打开的文件夹里找到名为 `hosts` 的文件，直接右键选择使用记事本方式打开即可。如果 etc 文件夹中并没有该文件，那么可能是隐藏了，设置显示即可。
  - 注，编辑后保存需要管理员权限。
- Step 5. 刷新 DNS 缓存
  - (1) 鼠标右键单击 win 键选择 `运行`
  - (2) 运行窗口输入 `cmd` 点击确定按钮，进入命令窗口
  - (3) 在命令提示符下输入 `ipconfig /flushdns`
  - (4) 回车后，命令执行成功
  - (5) 如果显示刷新失败，那么在运行中输入 `services.msc` 回车，进入服务列表
  - (6) 进入服务列表，找到 `DNS Client` 服务项双击
  - (7) 打开 DNS Client 服务项将启动类型设为自动，点击确定，重新第二步即可成功刷新
- refs:
  - [Win10系统hosts文件](https://blog.csdn.net/yang5726685/article/details/79360174)
  - [win10怎么刷新dns缓存](https://jingyan.baidu.com/article/91f5db1b0562b61c7e05e310.html)
- 注，DNS Client 右键前若干项可能均为灰色，此时 (后补)

Mac
- Step 4. 寻找 Hosts 文件的路径为
  - (1) Finder -> Go -> Go to Folder
  - (2) 输入 /etc/hosts 即可找到
- Step 5. 该文件一般编辑器打不开，可使用 NotePad++、SubLineText 等编辑器进行编辑





# References

