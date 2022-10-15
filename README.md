# Personal Blog

README_hugo.md


## restart

```shell
$ git branch
  hexo-next
* locate
  master
$ git branch -m hugo-road
$ git push origin --delete locate
To github.com:eustomaqua/eustomaqua.github.io.git
 - [deleted]         locate
$ git push origin -u hugo-road
$ git branch
  hexo-next
* hugo-road
  master
```

```shell
$ hugo new site blog
Congratulations! Your new Hugo site is created in /home/ubuntu/Homepage/eustomaqua.github.io/blog.

Just a few more steps and you\'re ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
$ ls
blog  hexo-next  README_hexo.md  README_hugo.md
$ ls blog
archetypes  config.toml  content  data  layouts  public  static  themes
$ mv blog hugo-blog
```

```shell
$ cd hugo-blog
$ git clone https://github.com/vimux/mainroad.git themes/mainroad
$ # git clone git clone https://github.com/xtfly/hugo-theme-next.git themes/next
$ git clone https://github.com/martignoni/hugo-notice.git themes/hugo-notice
$ hugo
$ hugo server

$ cd public && git init
$ git remote add origin git@github.com:eustomaqua/eustomaqua.github.io
$ git pull -f origin master
remote: Enumerating objects: 1709, done.
remote: Counting objects: 100% (421/421), done.
remote: Compressing objects: 100% (37/37), done.
remote: Total 1709 (delta 412), reused 384 (delta 384), pack-reused 1288
Receiving objects: 100% (1709/1709), 10.45 MiB | 2.12 MiB/s, done.
Resolving deltas: 100% (619/619), done.
From github.com:eustomaqua/eustomaqua.github.io
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
error: The following untracked working tree files would be overwritten by merge:
  categories/index.html
  categories/似此星辰/index.html
  css/main.css
  index.html
  music/AlecBenjamin-MatchInTheRain.lrc
  music/AlecBenjamin-ShadowOfMine.lrc
  tags/index.html
  tags/河图/index.html
Please move or remove them before you merge.
Aborting

$ git pull --rebase origin master
From github.com:eustomaqua/eustomaqua.github.io
 * branch            master     -> FETCH_HEAD
error: The following untracked working tree files would be overwritten by merge:
  categories/index.html
  categories/似此星辰/index.html
  css/main.css
  index.html
  music/AlecBenjamin-MatchInTheRain.lrc
  music/AlecBenjamin-ShadowOfMine.lrc
  tags/index.html
  tags/河图/index.html
Please move or remove them before you merge.
Aborting

$ cd .. && hugo && cd public
$ git add . && git commit -m "updated on date"
$ git push -f origin master
```

## refs

[Hugo 搭建博客实践, LiveRe](https://creaink.github.io/post/Devtools/Hugo/Hugo-intro.html)  
[为 Hugo 博客添加字数统计](https://mogeko.me/posts/zh-cn/033/)  
[Hugo添加短代码](https://www.zaqizaba.xyz/posts/hugo%E6%B7%BB%E5%8A%A0%E7%9F%AD%E4%BB%A3%E7%A0%81/)  
[Hugo博客添加音乐](http://www.y9.network/hugo%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E9%9F%B3%E4%B9%90/)  
[hugo搭建个人博客2-文章写作](https://shuzang.github.io/2019/hugo-blog-article-write/)  
[HUGO 使用概述](https://kuang.netlify.app/blog/hugo.html)  

[Theme Documentation - music Shortcode](https://hugoloveit.com/theme-documentation-music-shortcode/)  
[在hugo中添加音频 (useless)](https://blog.reez.me/posts/add_audio_to_hugo/)  
[在 Hugo 博客上实践 Shortcodes 短代码, 太强大了](https://matnoble.me/tech/hugo/shortcodes-practice-tutorial-for-hugo/)  
[使用不蒜子添加访客统计](https://blog.mikelyou.com/2020/08/18/busuanzi-visitor-counts-and-sitetime/)  
[Hugo代码增加显示行号功能](https://huangzhongde.cn/post/2020-02-22-hugo-code-linenumber/)  

[hugo-shortcodes-soundcloud](https://github.com/yuma-m/hugo-shortcodes-soundcloud)  
[How to embed a YouTube playlist in hugo website](https://stackoverflow.com/questions/72065012/how-to-embed-a-youtube-playlist-in-hugo-website)  
[How to nest shortcodes with Hugo? raw HTML ommitted](https://stackoverflow.com/questions/62129365/how-to-nest-shortcodes-with-hugo-raw-html-ommitted)  

