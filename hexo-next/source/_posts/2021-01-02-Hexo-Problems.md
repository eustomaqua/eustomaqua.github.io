---
title: Hexo+Next, Problem Solver
date: 2021-01-02 22:24:56
updated: 2021-01-02 22:24:56
categories:
  - Records
tags:
  - Hexo
mathjax: false
---


# 出现问题

## Next 主题布局配置

如果因为手误将主题的布局全注释了，即 `next/_config.yml` 中变成了
```yaml
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
#scheme: Gemini
```
那么 `hexo g` 就会出现报错信息
```shell
ERROR ENOENT: no such file or directory, open '/home/ubuntu/eustomaqua.github.io/hexo-next/themes/next/layout/_scripts/schemes/.swig'
```

### Comparison
<!-- 比较不同 -->
**可视化四种主题的布局以便于对比**

{% gp 1-3 %}
<img src="/images/2021-01/0102_NextSchemes_Muse1.png">
<img src="/images/2021-01/0102_NextSchemes_Muse2.png">
<img src="/images/2021-01/0102_NextSchemes_Muse3.png">
{% endgp %}
Scheme: Muse
{% gp 1-3 %}
<img src="/images/2021-01/0102_NextSchemes_Mist1.png">
<img src="/images/2021-01/0102_NextSchemes_Mist2.png">
<img src="/images/2021-01/0102_NextSchemes_Mist3.png">
{% endgp %}
Scheme: Mist
{% gp 1-3 %}
<img src="/images/2021-01/0102_NextSchemes_Pisces1.png">
<img src="/images/2021-01/0102_NextSchemes_Pisces2.png">
<img src="/images/2021-01/0102_NextSchemes_Pisces3.png">
{% endgp %}
Scheme: Pisces
{% gp 1-3 %}
<img src="/images/2021-01/0102_NextSchemes_Gemini1.png">
<img src="/images/2021-01/0102_NextSchemes_Gemini2.png">
<img src="/images/2021-01/0102_NextSchemes_Gemini3.png">
{% endgp %}
Scheme: Gemini

### Backup 援引
援引 {% post_link 2020-04-12-Hexo-Troubles %}

- 引用博文
  e.g., 引用文件夹 `_post/hello` 下的文件 `HelloWorld.md`
  ```markdown
  {% post_link hello/HelloWorld %}
  ```
- 多图模式
  ```markdown
  {% gp r-c %}
  <img src="/images/?.png">
  .... x n
  {% endgp %}
  ```
Options of `r-c`s
|***n***| results |***r-c***|  |  |
|-----|---------|-----|-----|-----|
|**2**|  **2**  | 1-2 |     |     |
|**3**|  **3**  | 1-3 | 1-2 |     |
|**4**| **2,2** | 4-3 | 5-3 |     |
|     | **3,1** | 6-5 | 8-7 | 5-4 |
|     | **3,?** | 1-4 | 1-5 |     |
|**5**| **2,3** | 5-3 | 7-4 |     |
|     |**2,1,2**| 5-2 | 6-3 |     |
|     | **3,2** | 8-7 |     |     |
|**6**|**2,1,3**| 6-3 |     |     |
|     |**2,3,1**| 7-4 |     |     |
|     |**2,2,2**| 7-3 |     |     |
|     | **3,3** | 8-7 |     |     |
|**7**|**2,3,2**| 8-5 |     |     |



## 侧边栏 posts 跳转异常
<!-- modified, 2021-01-02 22:24:56 -->

右侧 posts 莫名页面变成了 `http://localhost:4000/archives/%20%7C%7C%20archive/` 所以跳转失败，出错信息提示 `Cannot GET /archives/%20%7C%7C%20archive/`  

找到 `layout/_macro/sidebar.swig` 文件，找到第 48 行，原文为
```hexo
          {% if theme.site_state %}
            <nav class="site-state motion-element">
              {% if config.archive_dir != '/' and site.posts.length > 0 %}
                <div class="site-state-item site-state-posts">
                {% if theme.menu.archives %}
                  <a href="{{ url_for(theme.menu.archives).split('||')[0] | trim }}">
                {% else %}
```

### 修改 split 位置

第一次尝试：原因是url_for函数将||转码了，改为
```hexo
                {% if theme.menu.archives %}
                  <a href="{{ url_for(theme.menu.archives.split('||')[0]) | trim }}">
                {% else %}
                  <a href="{{ url_for(config.archive_dir) }}">
                {% endif %}
```
结果是变成了跳转 `http://localhost:4000/archives/ /` 得到 `Cannot GET /archives/%20/`  
**参考链接：**
[hexonext主题侧边栏日志出现问题](https://blog.csdn.net/qq_38765633/article/details/104929566)

第二次尝试：刚才发现是多了一个空格，因此改为
```hexo
                {% if theme.menu.archives %}
                  <a href="{{ url_for(theme.menu.archives.split('||')[0].strip()) | trim }}">
```
这样做的结果是发现回到了 Home 主页，即 `http://localhost:4000/`

<!--
然后再修改回最开始的状态，发现报错信息是
这是因为我手误将主题全注释了，即 `next/_config.yml` 中变成了
-->

### 删除中间的判断

仍是 `themes/next/layout/_macro/sidebar.swig` 文件

第 43-56 行原文为
```hexo
          {% if theme.site_state %}
            <nav class="site-state motion-element">
              {% if config.archive_dir != '/' and site.posts.length > 0 %}
                <div class="site-state-item site-state-posts">
                {% if theme.menu.archives %}
                  <a href="{{ url_for(theme.menu.archives).split('||')[0] | trim }}">
                {% else %}
                  <a href="{{ url_for(config.archive_dir) }}">
                {% endif %}
                    <span class="site-state-item-count">{{ site.posts.length }}</span>
                    <span class="site-state-item-name">{{ __('state.posts') }}</span>
                  </a>
                </div>
              {% endif %}
```

删除判断语句，即删除
```hexo
                {% if theme.menu.archives %}
                  <a href="{{ url_for(theme.menu.archives).split('||')[0] | trim }}">
                {% else %}

                {% endif %}
```

问题解决！
**参考链接：**
[Hexo+NexT搭建个人博客](https://lunachy.com/2020/05/09/Hexo+NexT%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)  
跳转 “侧栏中的posts打开的链接错误” 即可

### Some Refs

[侧边栏post链接跳转异常](https://github.com/iissnan/hexo-theme-next/issues/1836)  
[测试hexo4.0/next7.5出现的几个bug](https://github.com/hexojs/hexo/issues/3876)  
[fix(url_for & full_url_for): ignore data url](https://github.com/hexojs/hexo-util/pull/130)  

hexo posts archive 页面  
[怎么改变归档网页标题栏的'归档'两个字？](https://github.com/hexojs/hexo/issues/4065)  


# References

[YouTube Music Premium 使用感受](https://googlefanspost.blogspot.com/2018/12/youtube-music-premium.html)  
[Google Photos 和 Google Drive 的“共通”机制将不复存在](https://googlefanspost.blogspot.com/2019/06/google-photos-google-drive.html)  
