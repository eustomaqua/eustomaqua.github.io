---
title: Hexo+NexT, Localhost 网站找不到
date: 2020-04-24 15:12:26
updated: 2020-04-24 15:12:27
categories:
  - Records
tags:
  - Hexo
mathjax: false
---


# Hexo (框架)
## localhost 网页找不到

### Attempt 1: 仍在原来的文件夹内

起因是我不小心在 hexo-next 文件夹里用了 git add git commit ，本来应该是此文件夹的上层文件夹存储 git 的，而此文件夹只用 hexo g s d 等。结果就开始报错：
- 先是 hexo g, hexo s 都正常，但是本地 localhost 提示网页错误，可见下图
- 然后 hexo clean, hexo g ，就报错，lastIndex 相关的错误
- 于是我继续把 post 挪进挪出大法，hexo g 倒是没有问题了，但是 hexo s 仍然是 localhost 找不到此网站……
- 然后我在终端试了下 `ps -ef | grep 4000` 看是不是端口占用问题，没有问题，但是再 hexo s 就开始报错了……
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo s
FATAL Port 4000 has been used. Try other port instead.
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: listen EADDRINUSE 0.0.0.0:4000
    at Server.setupListenHandle [as _listen2] (net.js:1335:14)
    at listenInCluster (net.js:1383:12)
    at doListen (net.js:1509:7)
    at process._tickCallback (internal/process/next_tick.js:63:19)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```
  备注：其实上面换个端口的命令是 `hexo server -p 4001` ，不过我没试
- 把 ps 出现的那行进程杀掉，会发现此终端中止，在另一个终端里继续 hexo g hexo s，还是不行
- 然后我把虚拟机重启了……重启完还是不行
- 然后试了 `hexo s -p 4001` 进入 `http://localhost:4001/` 也不行
- 尝试重装 hexo-server 插件
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-server --save

> hexo-math@3.0.4 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-math
> cd ../.. && npm install --save hexo-inject

npm WARN deprecated hexo-inject@1.0.0: The author does not use Hexo any more. This plugin is no longer maintained.
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.

> core-js@2.6.11 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/babel-polyfill/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon: 
> https://opencollective.com/core-js 
> https://www.patreon.com/zloirock 

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)

+ hexo-inject@1.0.0
added 14 packages from 10 contributors, removed 5 packages, updated 19 packages and audited 3637 packages in 60.402s
found 203 vulnerabilities (136 low, 5 moderate, 62 high)
  run `npm audit fix` to fix them, or `npm audit` for details
+ hexo-server@0.2.2
added 8 packages from 3 contributors, removed 14 packages, updated 20 packages and audited 3576 packages in 80.264s
found 194 vulnerabilities (136 low, 4 moderate, 54 high)
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

<img src="/images/2020-04/0424_HexoServer_localhost.png" width="100%">
<br>

***Error log:***  
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo s
INFO  [hexo-math] Using engine 'mathjax'
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
TypeError: Cannot set property 'lastIndex' of undefined
    at highlight (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:511:35)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:561:21
    at Array.forEach (<anonymous>)
    at Object.highlightAuto (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:560:40)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:117:25
    at highlight (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:120:7)
    at highlightUtil (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:22:14)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:62:15
    at String.replace (<anonymous>)
    at Hexo.backtickCodeBlock (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:14:31)
    at Hexo.tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Hexo.<anonymous> (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/method.js:15:34)
    at Promise.each.filter (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/filter.js:63:65)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Object.gotValue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/reduce.js:155:18)
    at Object.gotAccum (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/reduce.js:144:25)
    at Object.tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromiseCtx (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:606:10)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:138:12)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 

ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  [hexo-math] Using engine 'mathjax'
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
TypeError: Cannot set property 'lastIndex' of undefined
    at highlight (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:511:35)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:561:21
    at Array.forEach (<anonymous>)
    at Object.highlightAuto (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/highlight.js/lib/highlight.js:560:40)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:117:25
    at highlight (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:120:7)
    at highlightUtil (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-util/lib/highlight.js:22:14)
    at /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:62:15
    at String.replace (<anonymous>)
    at Hexo.backtickCodeBlock (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/filter/before_post_render/backtick_code_block.js:14:31)
    at Hexo.tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Hexo.<anonymous> (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/method.js:15:34)
    at Promise.each.filter (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/filter.js:63:65)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Object.gotValue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/reduce.js:155:18)
    at Object.gotAccum (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/reduce.js:144:25)
    at Object.tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromiseCtx (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:606:10)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:138:12)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

### Attempt 2: 重建博客

奇怪的是，挪进挪出后， hexo g 正常，hexo s 仍然 localhost 网站找不到，但是 hexo d 正常了。然后继续分别 hexo s, hexo g 就会报上面两个错误。  
然后我把最后三篇日志挪出去，hexo g 正常；再逐篇分别挪回，hexo g 都没有问题；可是 hexo s 还是报上图的错误，换了端口也依然不行。  
查看 https://eustomaqua.github.io 会发现刚才添加的图片没有正常显示，其他的似乎还正常；现在问题就是本地无法 hexo s 查看了

最后我删掉 hexo-next 这个文件夹重新创建博客了……
```bash
# 1. 先备份之前的设置
$ cd eustomaqua.github.io/hexo-next
$ mv scaffolds ~/Documents/
$ mv source ~/Documents/
$ mv themes ~/Documents/
$ mv _config.yml ~/Documents/

# 2. 删除之前的文件
$ sudo rm -r *
$ cd ..
$ sudo rm -r hexo-next

# 3. 重新创建文件夹和进行依赖包的安装
$ mkdir hexo-next
$ cd hexo-next
$ hexo init
# 生成了 scaffolds, source, themes, _config.yml 三个文件夹和一个配置文件
$ sudo npm install
# 依赖包安装完成后，会多出 node_modules 一个文件夹和两个文件，即 package.json, package-lock.json

# 4. 测试初始化的博客
$ hexo g
$ hexo s
# 此时 http://localhost:4000/ 还是失败，找不到 localhost 的服务器
# 但是无意中尝试 http://127.0.0.1:4000/ 成功了

# 5. 移回之前的配置和博客等
$ ls ~/文档
$ mv ~/文档/themes/next ./themes/
$ mv ~/文档/_config.yml ./
$ hexo g
$ hexo s
# 这回 localhost 很慢，倒是 127.0.0.1 很快就好了，显示是正常的；
# 回头再看 localhost 发现它提示连接超时，可见下图

# 6. 继续移回之前的配置和博客等
$ rm -r themes/landscape
$ mv ~/文档/themes/landscape ./themes/
$ ls ~/文档  # source themes
$ ls ~/文档/themes  # empty
$ rm -r ~/文档/themes
$ ls ~/文档/source
categories  images  _legacy  _posts  tags
$ ls source
_posts
$ ls source/_posts
hello-world.md

$ cd source
$ mv _posts/* ./
$ mv ~/文档/source/* ./
$ rm -r ~/文档/source
$ ls
categories  hello-world.md  images  _legacy  _posts  tags
$ mv hello-world.md _legacy/
$ cd ..
# 从 ~/eustomaqua.github.io/hexo-next/source 回到上层文件夹
$ hexo g
$ hexo s
# localhost 依然是 `找不到此网站，我们无法连接至 localhost 的服务器`
# 127.0.0.1 无比正常

```
<img src="/images/2020-04/0424_HexoServer_timeout.png" width="100%">
<br>

***Error log:***
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ sudo rm -r hexo-next
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ ls
README.md
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ mkdir hexo-next
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ cd hexo-next
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo init
INFO  Cloning hexo-starter to ~/eustomaqua.github.io/hexo-next
正克隆到 '/home/ubuntu/eustomaqua.github.io/hexo-next'...
remote: Enumerating objects: 30, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 161 (delta 12), reused 12 (delta 4), pack-reused 131
接收对象中: 100% (161/161), 31.79 KiB | 0 bytes/s, 完成.
处理 delta 中: 100% (74/74), 完成.
检查连接... 完成。
子模组 'themes/landscape' (https://github.com/hexojs/hexo-theme-landscape.git) 未对路径 'themes/landscape' 注册
正克隆到 'themes/landscape'...
remote: Enumerating objects: 1063, done.
remote: Total 1063 (delta 0), reused 0 (delta 0), pack-reused 1063
接收对象中: 100% (1063/1063), 3.21 MiB | 1.35 MiB/s, 完成.
处理 delta 中: 100% (585/585), 完成.
检查连接... 完成。
子模组路径 'themes/landscape'：检出 '73a23c51f8487cfcd7c6deec96ccc7543960d350'
INFO  Install dependencies

> ejs@2.7.4 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/ejs
> node ./postinstall.js

Thank you for installing EJS: built with the Jake JavaScript build tool (https://jakejs.com/)

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

added 253 packages from 450 contributors and audited 470 packages in 23.112s
found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
INFO  Start blogging with Hexo!
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ sudo npm install
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

audited 470 packages in 4.874s
found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

\#\#\# Summary
## Summary
基本上，所有的资料 (***Refs:***) 都是要你改变端口号，说端口被占用了；但是其实，最后把 `http://localhost:4000/` 改成 `http://127.0.0.1:4000/` 就行了，端口号改变并无法解决我的问题。到最后，我也没能解决 localhost 的问题

(1) 但是重建博客后发现网站下方的 Total Words 不显示了...... *尝试恢复：*  
```bash
$ cd eustomaqua.github.io/hexo-next
$ npm install hexo-wordcount --save
$ npm uninstall hexo-symbols-count-time
# 查看 ./themes/next/layout/_partials/footer.swig 文件的 55-59 行左右
# 查看 ./_config.yml 文件的 wordcount 相应部分 (搜索关键词 wordcount)
# 查看 ./themes/next/_config.yml 文件的 wordcount 相应部分
$ hexo g  # 又生成了很多文件
$ hexo s  # 再打开 127.0.0.1:4000 就发现全站字数可以正常显示了
```

(2) 然而又发现换页的地方不正常，有代码出现……
- 这个搜了下大概是 Hexo 版本的问题
- 因为网站下方的版本显示的确有所不同
  - 之前是 `Total 136.9k Words | Powered by Hexo v3.7.1 | Theme — NexT.Mist v6.3.0`
  - 现在是 `Total 128.1k Words | Powered by Hexo v4.2.0 | Theme — NexT.Mist v6.3.0`
- ref: [<font color="green">翻页的地方显示不正常，有html代码</font>](https://github.com/Molunerfinn/hexo-theme-melody/issues/234)  

找到 `./themes/next/layout/_partials/pagination.swig` 文件，修改如下 (把`#`部分去掉注释)
```bash
{% if page.prev or page.next %}
  <nav class="pagination">
    {{
      paginator({
        prev_text: '<i class="fa fa-angle-left" aria-label="'+__('accessibility.prev_page')+'"></i>',
        next_text: '<i class="fa fa-angle-right" aria-label="'+__('accessibility.next_page')+'"></i>',
        mid_size: 1#,
        #escape  : false
      })
    }}
  </nav>
{% endif %}
```

(3) 又发现字数减少了，而且单篇的字数显示也有所不同，如倒数第二篇
- `In Records   |   3,927 words   |   18 minutes `
- `In Records   |   3.7k words   |   16 minutes `

***Refs:*** next 换页代码出现  
[翻页的地方显示不正常，有html代码](https://github.com/Molunerfinn/hexo-theme-melody/issues/234)  
[分页显示问题](https://github.com/hexojs/hexo/issues/3794)  
[pagination.swig](https://github.com/theme-next/hexo-theme-next/blob/master/layout/_partials/pagination.swig)  
[pagination parsing error 分页编译错误](https://github.com/hexojs/hexo/issues/3729)  

## Degrade hexo-wordcount

### No.1 Failed (with Error log)

hexo 降级 ref: [Github+Hexo+matery博客搭建小白教程](https://zhuanlan.zhihu.com/p/123286944)  
```bash
$ cd eustomaqua.github.io/hexo-next
$ hexo --version
$ npm install hexo@3.7.1
$ hexo g
$ hexo s
```
但是这样做了以后，单篇的 wordcount 形式仍然不对。应该是 hexo-wordcount 插件的问题了？

详细信息如下所示
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo --version
hexo: 4.2.0
hexo-cli: 1.1.0
os: Linux 4.15.0-96-generic linux x64
http_parser: 2.8.0
node: 10.6.0
v8: 6.7.288.46-node.13
uv: 1.21.0
zlib: 1.2.11
ares: 1.14.0
modules: 64
nghttp2: 1.32.0
napi: 3
openssl: 1.1.0h
icu: 61.1
unicode: 10.0
cldr: 33.0
tz: 2018c
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo@3.7.1
npm WARN deprecated fsevents@1.2.12: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/nunjucks/node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: abbrev@1.1.1 (node_modules/fsevents/node_modules/abbrev):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/abbrev' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.abbrev.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ansi-regex@2.1.1 (node_modules/fsevents/node_modules/ansi-regex):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/ansi-regex' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.ansi-regex.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: aproba@1.2.0 (node_modules/fsevents/node_modules/aproba):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/aproba' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.aproba.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: balanced-match@1.0.0 (node_modules/fsevents/node_modules/balanced-match):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/balanced-match' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.balanced-match.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: chownr@1.1.4 (node_modules/fsevents/node_modules/chownr):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/chownr' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.chownr.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: code-point-at@1.1.0 (node_modules/fsevents/node_modules/code-point-at):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/code-point-at' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.code-point-at.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: concat-map@0.0.1 (node_modules/fsevents/node_modules/concat-map):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/concat-map' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.concat-map.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: console-control-strings@1.1.0 (node_modules/fsevents/node_modules/console-control-strings):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/console-control-strings' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.console-control-strings.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: core-util-is@1.0.2 (node_modules/fsevents/node_modules/core-util-is):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/core-util-is' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.core-util-is.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: deep-extend@0.6.0 (node_modules/fsevents/node_modules/deep-extend):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/deep-extend' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.deep-extend.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: delegates@1.0.0 (node_modules/fsevents/node_modules/delegates):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/delegates' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.delegates.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: detect-libc@1.0.3 (node_modules/fsevents/node_modules/detect-libc):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/detect-libc' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.detect-libc.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fs.realpath@1.0.0 (node_modules/fsevents/node_modules/fs.realpath):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/fs.realpath' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.fs.realpath.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: has-unicode@2.0.1 (node_modules/fsevents/node_modules/has-unicode):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/has-unicode' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.has-unicode.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: inherits@2.0.4 (node_modules/fsevents/node_modules/inherits):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/inherits' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.inherits.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ini@1.3.5 (node_modules/fsevents/node_modules/ini):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/ini' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.ini.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: isarray@1.0.0 (node_modules/fsevents/node_modules/isarray):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/isarray' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.isarray.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: minimist@1.2.5 (node_modules/fsevents/node_modules/minimist):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/minimist' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.minimist.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ms@2.1.2 (node_modules/fsevents/node_modules/ms):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/ms' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.ms.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: npm-normalize-package-bin@1.0.1 (node_modules/fsevents/node_modules/npm-normalize-package-bin):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/npm-normalize-package-bin' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.npm-normalize-package-bin.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: number-is-nan@1.0.1 (node_modules/fsevents/node_modules/number-is-nan):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/number-is-nan' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.number-is-nan.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: object-assign@4.1.1 (node_modules/fsevents/node_modules/object-assign):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/object-assign' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.object-assign.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: os-homedir@1.0.2 (node_modules/fsevents/node_modules/os-homedir):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/os-homedir' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.os-homedir.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: os-tmpdir@1.0.2 (node_modules/fsevents/node_modules/os-tmpdir):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/os-tmpdir' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.os-tmpdir.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: path-is-absolute@1.0.1 (node_modules/fsevents/node_modules/path-is-absolute):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/path-is-absolute' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.path-is-absolute.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: process-nextick-args@2.0.1 (node_modules/fsevents/node_modules/process-nextick-args):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/process-nextick-args' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.process-nextick-args.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: safe-buffer@5.1.2 (node_modules/fsevents/node_modules/safe-buffer):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/safe-buffer' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.safe-buffer.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: safer-buffer@2.1.2 (node_modules/fsevents/node_modules/safer-buffer):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/safer-buffer' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.safer-buffer.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: sax@1.2.4 (node_modules/fsevents/node_modules/sax):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/sax' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.sax.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: semver@5.7.1 (node_modules/fsevents/node_modules/semver):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/semver' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.semver.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: set-blocking@2.0.0 (node_modules/fsevents/node_modules/set-blocking):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/set-blocking' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.set-blocking.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: signal-exit@3.0.2 (node_modules/fsevents/node_modules/signal-exit):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/signal-exit' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.signal-exit.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: strip-json-comments@2.0.1 (node_modules/fsevents/node_modules/strip-json-comments):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/strip-json-comments' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.strip-json-comments.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: util-deprecate@1.0.2 (node_modules/fsevents/node_modules/util-deprecate):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/util-deprecate' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.util-deprecate.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: wrappy@1.0.2 (node_modules/fsevents/node_modules/wrappy):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/wrappy' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.wrappy.DELETE'
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: yallist@3.1.1 (node_modules/fsevents/node_modules/yallist):
npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/yallist' -> '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/fsevents/node_modules/.yallist.DELETE'

+ hexo@3.7.1
added 196 packages from 85 contributors, removed 23 packages, updated 52 packages and audited 2613 packages in 52.129s
found 3 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

### 尝试降级 wordcount

(1) 基本命令
```bash
$ cd eustomaqua.github.io/hexo-next
$ npm install hexo-wordcount --save
$ hexo g
$ hexo s
```
发现最新的版本是 `hexo-wordcount@6.0.1`
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-wordcount --save
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/nunjucks/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-wordcount@6.0.1
updated 1 package and audited 2613 packages in 9.598s
found 3 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

(2) 降级尝试，失败
```bash
$ npm install hexo-wordcount@5.0.1 --save
$ npm install hexo-wordcount@5.9.* --save
```
即
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo s
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
^CINFO  Bye!
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-wordcount@5.0.1 --save
npm ERR! code ETARGET
npm ERR! notarget No matching version found for hexo-wordcount@5.0.1
npm ERR! notarget In most cases you or one of your dependencies are requesting
npm ERR! notarget a package version that doesn't exist.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/ubuntu/.npm/_logs/2020-04-24T07_29_02_166Z-debug.log
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-wordcount@5.9.* --save
npm ERR! code ETARGET
npm ERR! notarget No matching version found for hexo-wordcount@5.9.*
npm ERR! notarget In most cases you or one of your dependencies are requesting
npm ERR! notarget a package version that doesn't exist.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/ubuntu/.npm/_logs/2020-04-24T07_29_21_052Z-debug.log
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

(3) ***Refs:***  
[npm 安装指定版本（按版本安装）](https://blog.csdn.net/xuaner8786/article/details/81630445)  
[npm安装依赖至指定版本的方法](https://blog.csdn.net/yanzi1225627/article/details/80220408)  

Notice: **如何寻找插件的指定版本？**  
1. 打开官方网页 [https://www.npmjs.com/](https://www.npmjs.com/) 
2. 搜索插件名称，如 [hexo-wordcount](https://www.npmjs.com/search?q=hexo-wordcount)
3. 找到该插件的发布信息，如 [hexo-wordcount ReadMe](https://www.npmjs.com/package/hexo-wordcount)
4. 点击右侧的 `18 Versions`，可获知历次更新的版本信息，从中寻找即可
5. 例如 hexo-wordcount 会发现其最新版是 `6.0.1`，之前的版本分别是 `6.0.0` 和 `5.0.0`，所以先尝试 `npm install hexo-wordcount@5.0.0 --save`，若不行再继续往下降级尝试
6. 很幸运，`hexo-wordcount@5.0.0` 就是要寻找的版本，现在字数的展示形式恢复了

总结：hexo-wordcount 6.0.1 的字数统计完之后会比 5.0.0 的略少一些，此外 6.0.1 在单篇中不能展示具体数值。

```bash
$ cd eustomaqua.github.io/hexo-next
$ npm install hexo-wordcount@5.0.0 --save
```
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-wordcount@5.0.0 --save
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/nunjucks/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-wordcount@5.0.0
added 9 packages from 15 contributors, updated 1 package and audited 2627 packages in 13.116s
found 4 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

# Hexo (框架)

## git not found
ref: [hexo d命令报错 ERROR Deployer not found: git](https://blog.csdn.net/qq_21808961/article/details/84476504)

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo d
ERROR Deployer not found: git
```

错因：没有安装 `hexo-deployer-git` 插件，安装就好了，
然后再推送 `hexo d` 即可
```bash
$ npm install hexo-deployer-git --save
```

Details:
```powershell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-deployer-git --save
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/hexo-deployer-git/node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/nunjucks/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-deployer-git@2.1.0
added 48 packages from 30 contributors and audited 2727 packages in 19.902s
found 5 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

# Refs
