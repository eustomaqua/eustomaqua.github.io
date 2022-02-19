# Personal Blog

Summary  
[OneDrive直链获取工具v1.3](https://onedrive.gimhoy.com/)  
[歌曲LRC滚动歌词在线生成制作编辑器软件](https://www.yuanchuangyinyue.com/3027.html)  
```shell
$ cd hexo-next
$ hexo g
$ hexo s
$ hexo d
```


# Personal Blog

```shell
$ cd eustomaqua.github.io
$ npm install --save hexo-pdf
```

[HEXO博客中插入PDF](https://www.jianshu.com/p/111452a36e94)  
[hexo中插入pdf解决方法](http://miracle778.site/pdf-test/pdf-test.html)  
[后端 hexo 中如何插入pdf插件(傻瓜教程)](https://www.dazhuanlan.com/parischen/topics/1572910)  
[hexo-部署出错at formatNunjucksError](https://www.wztlink1013.com/blog/gw1d4z/)  
[hexo 大坑](https://godliuyang.wang/2019/07/22/hexo-da-keng/)  


## Config

```shell
$ cd /media/sf_GitD
$ git clone git@github.com:eustomaqua/eustomaqua.github.io.git
$ git checkout hexo-next
$ git checkout -b office

$ # sudo apt-get install nodejs
$ # sudo apt-get install npm
$ # sudo apt-get purge nodejs
$ # sudo apt autoremove

$ sudo apt-get install curl
$ curl -fsSL https://deb.nodesource.com/setup_17.x | sudo -E bash -
$ git branch -m office locate
$ git branch
```

after node.js
```shell
$ # git clone git@github.com:electron/electron-quick-start.git
$ # cd electron-quick-start
$ # npm install
$ # npm start
$ rm -r electron-quick-start

$ sudo npm install hexo-cli -g
$ su
# npm install hexo-generator-index
# npm install hexo-generator-archive
# npm install hexo-generator-tag
# npm install hexo-generator-category
# exit
```

blog
```shell
$ cd hexo-next
$ sudo npm install
$ cd ..
$ npm install
$ npm install hexo-deployer-git

$ cd ~/eustomaqua.github.io
$ npm install hexo
$ npm install
$ npm install hexo-deployer-git

$ rm -r package-lock.json
$ rm -r package.json
$ rm -r npm-debug.log.3530940769

$ git status
$ git push --set-upstream origin locate

$ cd hexo-next
$ hexo g
$ hexo s
$ hexo clean
```

plugins
```shell
$ npm install hexo-generator-feed
$ npm install hexo-generator-index
$ npm install hexo-generator-archive
$ npm install hexo-generator-tag
$ npm install hexo-generator-category
$ npm install hexo-generator-sitemap
$ npm install hexo-generator-baidu-sitemap
$ npm fund
eustomaqua.github.io
├── https://github.com/sponsors/ljharb
│   └── is-core-module@2.8.0
└── https://github.com/fb55/domhandler?sponsor=1
    └── domhandler@4.3.0

$ npm install is-core-module
$ cd hexo-next
$ sudo npm install
```

```shell
$ hexo g
$ hexo s  # http://localhost:4000
$ hexo d

$ sudo lsof -i :4000
$ kill -15 PID
```

[如何在Hexo中对文章md文件分类](https://www.githang.com/2018/12/22/hexo-new-post-path/)  

Port 4000 has been used. Try other port instead
[FATAL Port 4000 has been used. Try other port instead.](https://blog.csdn.net/Caiqiudan/article/details/109954422)  
[hexo搭建博客过程中出现的问题，4000端口被占用](https://segmentfault.com/q/1010000008546859)  
https://hexo.io/docs/troubleshooting.html
[listen EADDRINUSE: address already in use :::4000](https://github.com/the-couch/slater/issues/84)  
[address already in use :::4000](https://stackoverflow.com/questions/65506937/error-listen-eaddrinuse-address-already-in-use-4000)  

```shell
$ sudo n 10.6.0
[sudo] ubuntu 的密码： 
  installing : node-v10.6.0
       mkdir : /usr/local/n/versions/node/10.6.0
       fetch : https://nodejs.org/dist/v10.6.0/node-v10.6.0-linux-x64.tar.xz
   installed : v10.6.0 (with npm 6.1.0)

$ vim ~/.bashrc
$ source ~/.bashrc
$ cd hexo-next
$ git init

$ hexo g
$ hexo s
$ hexo d

$ node -v
v10.6.0
$ npm -v
6.1.0

$ rm -r .git
$ cd ..
$ git status
```

[部署Hexo踩过的坑—node14.0配置hexo](https://zhuanlan.zhihu.com/p/136552969)  



## Node.js

[Ubuntu 16.04 安装 node](https://www.jianshu.com/p/91cd8c0a26ca)  
[How To Install Node.js on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)  
[如何在Ubuntu 16.04上安装Node.js](https://cloud.tencent.com/developer/article/1352622)  
[如何在 Ubuntu 20.04 上安装 Node.js 和 npm](https://developer.aliyun.com/article/760687)  
[Vue 学习(五、扩展 - 安装 Node.js 运行环境 和 NPM 操作总结)](https://blog.csdn.net/Ares5kong/article/details/121537852)  
[Ubuntu apt-get彻底卸载软件包](https://blog.csdn.net/get_set/article/details/51276609)  
```shell
$ sudo apt-get install nodejs
$ sudo apt install nodejs-legacy
$ sudo apt install npm
$ node -v  # v4.2.6
$ npm -v   # 3.5.2

$ sudo npm config set registry https://registry.npm.taobao.org
$ sudo npm config list
$ sudo npm install n -g

$ sudo n stable
 installing : node-v16.13.1
       mkdir : /usr/local/n/versions/node/16.13.1
       fetch : https://nodejs.org/dist/v16.13.1/node-v16.13.1-linux-x64.tar.xz
   installed : v16.13.1 (with npm 8.1.2)

Note: the node command changed location and the old location may be remembered in your current shell.
         old : /usr/bin/node
         new : /usr/local/bin/node
To reset the command location hash either start a new shell, or execute PATH="$PATH"

$ sudo n latest
  installing : node-v17.2.0
       mkdir : /usr/local/n/versions/node/17.2.0
       fetch : https://nodejs.org/dist/v17.2.0/node-v17.2.0-linux-x64.tar.xz
   installed : v17.2.0 (with npm 8.1.4)

$ sudo n 10.15.1
  installing : node-v10.15.1
       mkdir : /usr/local/n/versions/node/10.15.1
       fetch : https://nodejs.org/dist/v10.15.1/node-v10.15.1-linux-x64.tar.xz
   installed : v10.15.1 (with npm 6.4.1)

$ echo PATH
$ vim ~/.bashrc
export PATH="/usr/local/n/versions/node/16.3.1:$PATH"
$ source ~/.bashrc
$ node -v  # v10.15.1
$ npm -v   # 8.1.2 or 6.4.1
```

[Node.js installation failed](https://github.com/nodesource/distributions/blob/master/README.md)  
```shell
$ sudo add-apt-repository -y -r ppa:chris-lea/node.js
$ sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list
$ sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list.save

$ KEYRING=/usr/share/keyrings/nodesource.gpg
$ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | sudo tee "$KEYRING" >/dev/null
$ gpg --no-default-keyring --keyring "$KEYRING" --list-keys
gpg: /home/ubuntu/.gnupg/trustdb.gpg：建立了信任度数据库
/usr/share/keyrings/nodesource.gpg
----------------------------------
pub   4096R/68576280 2014-06-13
uid                  NodeSource <gpg@nodesource.com>
sub   4096R/AA01DA2C 2014-06-13

$ DISTRO="$(lsb_release -s -c)"
$ echo "deb [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee /etc/apt/sources.list.d/nodesource.list
deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/ xenial main
$ echo "deb-src [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee -a /etc/apt/sources.list.d/nodesource.list
deb-src [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/ xenial main

$ sudo apt-get update
$ sudo apt-get install nodejs
$ nodejs -v
v4.2.6

$ sudo apt-get purge nodejs
$ sudo apt autoremove
```
backup log
```shell
ubuntu@ubuntu-VirtualBox:/media/sf_GitD$ git clone git@github.com:eustomaqua/eustomaqua.github.io.git
正克隆到 'eustomaqua.github.io'...
ssh: /home/ubuntu/Software/anaconda3/lib/libcrypto.so.1.0.0: no version information available (required by ssh)
ssh: /home/ubuntu/Software/anaconda3/lib/libcrypto.so.1.0.0: no version information available (required by ssh)
remote: Enumerating objects: 4623, done.
remote: Counting objects: 100% (3060/3060), done.
remote: Compressing objects: 100% (444/444), done.
remote: Total 4623 (delta 1535), reused 2973 (delta 1497), pack-reused 1563
接收对象中: 100% (4623/4623), 30.84 MiB | 5.74 MiB/s, 完成.
处理 delta 中: 100% (1783/1783), 完成.
检查连接... 完成。
ubuntu@ubuntu-VirtualBox:/media/sf_GitD$ cd eustomaqua*
ubuntu@ubuntu-VirtualBox:/media/sf_GitD/eustomaqua.github.io$ git branch
* master
ubuntu@ubuntu-VirtualBox:/media/sf_GitD/eustomaqua.github.io$ git checkout hexo-next
分支 hexo-next 设置为跟踪来自 origin 的远程分支 hexo-next。
切换到一个新分支 'hexo-next'
ubuntu@ubuntu-VirtualBox:/media/sf_GitD/eustomaqua.github.io$ git checkout -b office
切换到一个新分支 'office'
ubuntu@ubuntu-VirtualBox:/media/sf_GitD/eustomaqua.github.io$
```
