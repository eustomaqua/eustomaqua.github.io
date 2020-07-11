---
title: Hexo 音视频的插入
date: 2020-07-11 13:43:37
updated: 2020-07-11 13:43:37
categories:
  - Records
tags:
  - Hexo
mathjax: false
---




# 插入音乐视频

## 使用 APlayer 插件插入音乐

进入 blog 根目录，安装 Aplayer 插件
```bash
$ npm install hexo-tag-aplayer --save
```

按照下面写法，将自己想要放上去的音乐插入即可
```html
{% aplayer "歌曲名" "歌手名" "歌曲的链接，如http://什么什么什么的.mp3" "http://封面图.jpg" "lrc:http://歌词.lrc" %}
```

### Details:
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-tag-aplayer --save
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.

> core-js@2.6.11 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/babel-polyfill/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon: 
> https://opencollective.com/core-js 
> https://www.patreon.com/zloirock 

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)


> core-js@2.6.11 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/babel-runtime/node_modules/core-js
> node -e "try{require('./postinstall')}catch(e){}"

npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/nunjucks/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/hexo-deployer-git/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-tag-aplayer@3.0.4
added 16 packages from 203 contributors and audited 569 packages in 30.597s
found 8 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```


## 使用 DPlayer 插件插入视频

安装
```bash
$ npm install --save hexo-tag-dplayer
```

博客中写法:  
要使用弹幕，必须有 api 和 id 两项, id 的值可以自己随意取，api 可以直接使用上方的官网 api
```html
{% dplayer "url=https://什么什么什么.mp4" "https://封面图.jpg" "api=https://api.prprpr.me/dplayer/" "id=" "loop=false" %}
```

示例 
```markdown
{% dplayer key=value ... %}
```
```html
{% dplayer "url=http://www.nenu.edu.cn/_upload/article/videos/03/5f/7c999eed42e3aadc413d7f851f0e/0f50b3eb-9285-41d2-ac4d-6cc363651aad_B.mp4"  "autoplay=true" "preload=metadata" "hotkey=true" %}
```

### Details

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-tag-dplayer --save
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/nunjucks/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.1.3 (node_modules/hexo-deployer-git/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-tag-dplayer@0.3.3
added 8 packages from 11 contributors and audited 577 packages in 20.487s
found 9 low severity vulnerabilities
  run `npm audit fix` to fix them, or `npm audit` for details


   ╭────────────────────────────────────────────────────────────────╮
   │                                                                │
   │       New minor version of npm available! 6.1.0 → 6.14.6       │
   │   Changelog: https://github.com/npm/npm/releases/tag/v6.14.6   │
   │               Run npm install -g npm to update!                │
   │                                                                │
   ╰────────────────────────────────────────────────────────────────╯

ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

## APlayer

用法
```markdown
{% aplayer title author url [picture_url, narrow, autoplay, width:xxx, lrc:xxx] %}
```

参数
```html
title ：音乐标题
author：音乐作者
url：音乐文件网址
picture_url：可选，音乐图片网址
narrow：可选，窄款式
autoplay：可选，自动播放音乐，不支持移动浏览器
width:xxx：可选，前缀width:，播放器宽度（默认值：100％）
lrc:xxx：可选，前缀lrc:，LRC文件url
```
```markdown
{% aplayer "Caffeine" "Jeff Williams" "caffeine.mp3" "picture.jpg" "lrc:caffeine.txt" %}
```

播放列表
```markdown
{% aplayerlist %}
{
    "narrow": false,                 // Optional, narrow style
    "autoplay": true,                // Optional, autoplay song(s), not supported by mobile browsers
    "mode": "random",                // Optional, play mode, can be `random` `single` `circulation`(loop) `order`(no loop), default: `circulation`
    "showlrc": 3,                    // Optional, show lrc, can be 1, 2, 3
    "mutex": true,                   // Optional, pause other players when this player playing
    "theme": "#e6d0b2",              // Optional, theme color, default: #b7daff
    "preload": "metadata",           // Optional, the way to load music, can be 'none' 'metadata' 'auto', default: 'auto'
    "listmaxheight": "513px",        // Optional, max height of play list
    "music": [
        {
            "title": "CoCo",
            "author": "Jeff Williams",
            "url": "caffeine.mp3",
            "pic": "caffeine.jpeg",
            "lrc": "caffeine.txt"
        },
        {
            "title": "アイロニ",
            "author": "鹿乃",
            "url": "irony.mp3",
            "pic": "irony.jpg"
        }
    ]
}
{% endaplayerlist %}
```

## DPlayer

# Summary

[音乐直链搜索工具](https://music.liuzhijin.cn/)  
[Hexo全局添加APlayer音乐播放器](https://linbei.top/Hexo%E5%85%A8%E5%B1%80%E6%B7%BB%E5%8A%A0APlayer%E9%9F%B3%E4%B9%90%E6%92%AD%E6%94%BE%E5%99%A8/)  
[hexo 插入音乐与视频](http://eternalzttz.com/hexoMV.html)  


# References

Less use  
[Aplayer \& Dplayer 嵌入音频和视频](https://mackvord.github.io/aplayer-dplayer/547187035.html)  
[Hexo主题插入音乐之aplayer音乐播放器](https://blog.csdn.net/hushhw/java/article/details/88092728)  
[在Hexo搭建的博客中插入音乐或者视频](https://datablog.top/2019/04/25/hexo-with-music-and-movie/)  
[请问如何能将player居中 调整宽度后默认在左边](https://github.com/MoePlayer/hexo-tag-aplayer/issues/42)  
[Aplayer搭配MetingJS音乐插件的使用](https://www.shuzhiduo.com/A/Gkz1wBp25R/)  
[安装和使用Dplayer](https://blog.csdn.net/weixin_43360634/article/details/97392613)  

No use  
[Hexo使用APlayer插入音乐](https://louisnie.github.io/2019/06/26/Hexo%20%E4%BD%BF%E7%94%A8%20APlayer%20%E6%8F%92%E5%85%A5%E9%9F%B3%E4%B9%90/)  
[如何给博客加上音乐](https://juejin.im/post/5c7ba2b4e51d45619d255b1d)  
[Hexo博客添加背景音乐和音乐歌单](http://blog.leroy.net.cn/2019/10/17/hexo-next-%E9%9F%B3%E4%B9%90/)  



# Hexo: 端口 4000 被占用

```bash
$ netstat -tunlp | grep 4000
$ kill -9 [process-id]
$
$ # ps -ef | grep 4000
$ # lsof -i:4000
```


