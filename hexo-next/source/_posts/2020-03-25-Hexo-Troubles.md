---
title: Hexo+NexT, Trouble Solver
date:
updated: 2020-03-25 21:36:22
categories:
  - Records
tags:
  - Hexo
  - Debug
  - LaTeX
  - Markdown
  - Git
---



<!--
date: 2020-03-25 03:53:56
updated: 2020-03-25 21:36

SHOW:
Post on __25 Mar 2020
Created 25 Mar 2020 09:21:22 / Modified: 21:36:00

updated: 2020-03-25 21:36:22
-->
[Hexo Official: Troubleshooting](https://hexo.io/docs/troubleshooting.html)  
Hexo (一个快速、简洁且高效的博客框架) 使用中所遇到的一些问题,  
e.g., ``FATAL``; `YAMLException: imcomplete explicit mapping pair`, etc.

\#\# 排查方法是先找到出错的日志（其实基本上就是最新一篇），然后依次从少到多增加其中的各行代码，寻找/定位哪部分出了错。
<!--2020-03-24-Matplotlib-Tutorial-Gallery.md-->

# Hexo (框架)

Nearly useless: [YAMLException: incomplete explicit mapping pair](https://stackoverflow.com/questions/37010777/yamlexception-incomplete-explicit-mapping-pair)

> **Template render error**
> Sometimes when running the command $ hexo generate it returns an error:
> ```bash
  FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
  Template render error: (unknown path)
  ```
> It means that there are some unrecognizable words in your file, e.g. invisible zero width characters. There are two possibilities One is your new page/post, and the other one is _config.yml.
> In `_config.yml`, don’t forget add whitespace before a list in hash. There is the wiki page about YAML.
The error one:

>

## 多图模式 `{\% end gp \%}`; 字符`_`反转义
i.e., 多图模式不能写成 `{\% end gp \%}`; 和 `_` 字符使用时需反转义

找到的有两类错误，
(1) markdown 中的 `_` 没有反转义，如
```markdown
### boxplot_vs_violin_demo
[statistics example code: boxplot_vs_violin_demo.py](https://matplotlib.org/examples/statistics/boxplot_vs_violin_demo.html) 
<img src="https://matplotlib.org/_images/boxplot_vs_violin_demo.png" width="87%">
```
(2) 应该是 `endgp`, 其中 `end` 和 `gp` 之间没有空格
```markdown
{% gp 1-2 %}
{% end gp %}
```

### Error log (错误日志) of Two
#### FATAL Something's wrong
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo clean
INFO  Deleted database.
INFO  Deleted public folder.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 32, Column 2]
  unknown block tag: end
    at Object._prettifyError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/lib.js:36:11)
    at Template.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:524:21)
    at Environment.renderString (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:362:17)
    at Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:66:9)
    at Promise._execute (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/debuggability.js:303:9)
    at Promise._resolveFromExecutor (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/post.js:230:16)
    at Promise.then.then.result (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/render.js:65:19)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:696:18)
    at tryOnImmediate (timers.js:667:5)
    at processImmediate (timers.js:649:5)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```
#### YAMLException: imcomplete explicit mapping pair
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo clean
INFO  Deleted database.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
ERROR Process failed: _posts/2020-03-25-Hexo-Troubles.md
YAMLException: incomplete explicit mapping pair; a key node is missed; or followed by a non-tabulated empty line at line 1, column 17:
    title: Hexo+NexT: Trouble Solver
                    ^
    at generateError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:165:10)
    at throwError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:171:9)
    at readBlockMapping (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1000:9)
    at composeNode (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1332:12)
    at readDocument (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1492:3)
    at loadDocuments (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1548:5)
    at Object.load (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1569:19)
    at parseYAML (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:80:21)
    at parse (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:56:12)
    at Promise.all.spread (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/processor/post.js:52:20)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:509:35)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Promise._fulfill (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:638:18)
    at PromiseArray._resolve (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:126:19)
    at PromiseArray._promiseFulfilled (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:144:14)
    at PromiseArray._iterate (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:114:31)
    at PromiseArray.init [as _init] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:78:10)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:566:21)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 32, Column 2]
  unknown block tag: end
    at Object._prettifyError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/lib.js:36:11)
    at Template.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:524:21)
    at Environment.renderString (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:362:17)
    at Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:66:9)
    at Promise._execute (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/debuggability.js:303:9)
    at Promise._resolveFromExecutor (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/post.js:230:16)
    at Promise.then.then.result (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/render.js:65:19)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:696:18)
    at tryOnImmediate (timers.js:667:5)
    at processImmediate (timers.js:649:5)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

## 冒号字符不可出现在标题中

出错代码
```markdown
---
title: Hexo+NexT: Trouble Solver
date: 
updated: 2020-03-25 21:36
categories:
  - Records
tags:
  - Hexo
  - Debug
---
```

**Error log**
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
ERROR Process failed: _posts/2020-03-25-Hexo-Troubles.md
YAMLException: incomplete explicit mapping pair; a key node is missed; or followed by a non-tabulated empty line at line 1, column 17:
    title: Hexo+NexT: Trouble Solver
                    ^
    at generateError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:165:10)
    at throwError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:171:9)
    at readBlockMapping (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1000:9)
    at composeNode (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1332:12)
    at readDocument (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1492:3)
    at loadDocuments (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1548:5)
    at Object.load (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1569:19)
    at parseYAML (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:80:21)
    at parse (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:56:12)
    at Promise.all.spread (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/processor/post.js:52:20)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:509:35)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Promise._fulfill (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:638:18)
    at PromiseArray._resolve (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:126:19)
    at PromiseArray._promiseFulfilled (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:144:14)
    at PromiseArray._iterate (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:114:31)
    at PromiseArray.init [as _init] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:78:10)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:566:21)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
INFO  Files loaded in 3.31 s
INFO  0 files generated in 12 s
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

## 百分号`\%`出现在大括号`{}`中需反转义
i.e., 百分号 `\%` 出现在行间代码中需反转义

出错行代码
```markdown
## 多图模式不能写成 `{% end gp %}`; `_` 字符使用时需反转义
```

修改后可发现是第一行出了问题
```markdown
## 多图模式不能写成 `\{% end gp %\}`
## `_` 字符使用时需反转义
```

这里面的错误是 百分号 `\%` 没有反转义，应该写成下面的第一行形式。不过将大括号同时反转义也可以
```markdown
## 多图模式不能写成 `{\% end gp \%}`
## 多图模式不能写成 `\{\% end gp \%\}`
```

注意这里百分号是如果出现在 markdown 小标题里的行间代码，就要<!--加上转义字符，-->反转义；如果是在普通文字内容里的行间代码，不用反转义。如 ·`%` 。  

**\[补充\]** `%` 需要反转义的情形是，需同时满足：
(1) 出现在行间代码中，不管是小标题还是普通文字内容；
(2) 出现在大括号 `{}` 中
这里的意思其实是认为 `%` 已经出现在代码文件里了，而 `%` 可能是某些编程语言的注释符号 (如 MATLAB)，所以需要反转义。
以上是我的猜测。

**Error log**
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 9, Column 113]
  unknown block tag: end
    at Object._prettifyError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/lib.js:36:11)
    at Template.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:524:21)
    at Environment.renderString (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:362:17)
    at Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:66:9)
    at Promise._execute (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/debuggability.js:303:9)
    at Promise._resolveFromExecutor (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/post.js:230:16)
    at Promise.then.then.result (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/render.js:65:19)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:696:18)
    at tryOnImmediate (timers.js:667:5)
    at processImmediate (timers.js:649:5)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

## 文中出现`#`时需反转义,不能直接使用
这里的错误是 \# 字符没有反转义，所以要么让它变成行间代码，要么就反转义一下。  

*出错代码/修改后代码*
```markdown
**1, 页内超链接:**
`` `markdown
# 1.分级目录{\#index}
  跳转到[标题]{\#index}
`` `
说明：在你准备跳转到的指定标题后插入锚点 `{\#标记}`，然后在文档的其它地方写上连接到锚点的链接。此处使用的是 GitHub 风格的 Markdown 语法所以无法正常显示效果，推荐使用以下 `2, 文章内部标题链接`。
```

*修改后显示 e.g.,*
```markdown
# 1.分级目录{\#index}
  跳转到[标题]{\#index}
```
说明：在你准备跳转到的指定标题后插入锚点 `{\#标记}`，然后在文档的其它地方写上连接到锚点的链接。此处使用的是 GitHub 风格的 Markdown 语法所以无法正常显示效果，推荐使用以下 `2, 文章内部标题链接`。
<!--font color="bluebird"-->

**Error log**
```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo s
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
Unhandled rejection Template render error: (unknown path)
  Error: expected end of comment, got end of file
    at Object._prettifyError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/lib.js:36:11)
    at Template.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:524:21)
    at Environment.renderString (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:362:17)
    at Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:66:9)
    at Promise._execute (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/debuggability.js:303:9)
    at Promise._resolveFromExecutor (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/post.js:230:16)
    at Promise.then.then.result (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/render.js:65:19)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:696:18)
    at tryOnImmediate (timers.js:667:5)
    at processImmediate (timers.js:649:5)

^CINFO  Have a nice day
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path)
  Error: expected end of comment, got end of file
    at Object._prettifyError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/lib.js:36:11)
    at Template.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:524:21)
    at Environment.renderString (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/nunjucks/src/environment.js:362:17)
    at Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:66:9)
    at Promise._execute (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/debuggability.js:303:9)
    at Promise._resolveFromExecutor (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/post.js:230:16)
    at Promise.then.then.result (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/hexo/render.js:65:19)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:696:18)
    at tryOnImmediate (timers.js:667:5)
    at processImmediate (timers.js:649:5)
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```


## Questions?


# NexT Theme (主题)

## Posted 日期问题

i) 每篇日志下方会出现形如 **``Post on Date``** 字样，有下列几种情况：
- 如果更新日期与创建日期不在同一天，那么会出现
  -- 显示 `Posted on 07 Jul 2018 | Edited on 25 Mar 2020`
  -- 鼠标悬停到对应位置，可以出现相应的时间，精确到秒
- 更新日期与创建日期在同一天，但处于不同时刻
  -- 显示 ``Posted on 08 Jul 2018``
  -- 鼠标 ``Created: 08 Jul 2018 13:44:55 / Modified: 23:41:52``
- 更新日期与创建日期在同一天的同一时刻
  -- 显示 `Posted on 07 Jul 2018`
  -- 鼠标 `Created: 07 Jul 2018 16:51:10`

`date:` 影响排序位置，而 `updated:` 只是做个注解。  
因此我们可以根据这两个时间的填写来判断一些自定义的特殊情形，比如说在我的设定中：  
-- 对于某些可能会经多次更新的文章，可以把创建时间填入 `update:` 位置，空置 `date:`，这样修改后该文章就可以出现在比较靠前的地方了。
-- 如果发现 `.md` 中 `date:` 和 `updated:` 的时间一模一样，就可以认为是这篇文章即使后来有修改，但是也没有必要特别留意记录修改时间了。

<!--
<ul style="line-height: 1.5em; list-style-type: square;"><li>对于某些可能会经多次更新的文章，可以把创建时间填入 `update:` 位置，空置 `date:`，这样修改后该文章就可以出现在比较靠前的地方了。</li><li>如果发现 `.md` 中 `date:` 和 `updated:` 的时间一模一样，就可以认为是这篇文章即使后来有修改，但是也没有必要特别留意记录修改时间了。</li></ul>

\* 对于某些可能会经--需要--多次更新的文章，可以把创建时间填入 'update:' 位置，空置 'date:'，这样修改后该文章就可以出现在比较靠前的地方了。  
\+ 如果发现 '.md' 中 'date:' 和 'updated:'' 的时间一模一样，就可以认为是这篇文章即使后来有修改，但是也没有必要特别--特意/特别留意--留意记录修改时间了。
-->

**注意：** 在 `.md` 文件开头里的两个日期位置，
> ```markdown
---
title: Title of Daily Diary
date: 2018-07-07 16:51:10
updated:
categories:
  - Category
tags:
  - Tag
---
```

<u>如果只填写了 `date:` , 而 `updated:` 后不管是空白不填还是直接删掉</u>，都不影响 hexo 自动生成相应的时间，这个时间应该是根据此 md 文件对应的 html 生成的时间，如果 md 有改动，html 就会重新生成，这时自动记录的就是 `Edited on`。  
<u>如果空置 `date:` 而填写 `updated:`</u>，那么 date 时间也是类似确定，由 hexo g 过程中自动生成。

ii) 我对<u>日期的填写</u>通常有 ***四种可能*** 方式：
- 两个都填写到秒（最常规普遍的情况）
- 空置 ``date`` 只填写 ``update``
  - 出现 `Posted on AutomatedTime / Modified: FixedSpecific`  
    这里后者时间是固定不变的，前者自动化生成
  - e.g., 显示 `Posted on 25 Mar 2020` <!--悬停位置-->
    鼠标悬停 `Created: 25 Mar 2020 11:01:07 / Modified: 21:36:22`
- 填写 ``date``，空白 ``update``
  - e.g., 显示 `Posted on 24 Mar 2020 | Edited on 25 Mar 2020`
    鼠标 Posted: `Created: 24 Mar 2020 23:31:03`
    鼠标 Edited: `Modified: 25 Mar 2020 09:35:32`
- 填写 ``date``，删掉 ``update`` 字段 (效果同 *空白 `update`*)
  - e.g., 显示 `Posted 07 Jul 2018 | Edited on 25 Mar 2020`
    鼠标 Posted: `Created: 07 Jul 2018 16:51:10`
    鼠标 Edited: `Modified: 25 Mar 2020 10:37:23`

<!--
而预留日期精确到哪一位也略有不同<! --/有所不同- - >：
- 预留时间写到秒
  e.g., ` ` `markdown
  ` ` `
-->

而预留日期精确到哪一位也略有不同：
- 预留时间写到秒
  e.g., 
  > ```markdown
  date:
  updated: 2020-03-25 21:36:22
  ```
  -- 显示同上
  -- 鼠标 `Created: / Modified: 21:36:22` 

- 预留时间只写到了分钟，而未精确到秒
  e.g., 
  > ```markdown
  date:
  updated: 2020-03-25 21:36
  ```
  -- 显示 `Posted on 25 Mar 2020`
  -- 鼠标 `Created: 25 Mar 2020 11:01:07 / Modified: 21:36:00`
- 预留时间只写到小时
  e.g., 
  > ```markdown
  date: 
  updated: 2020-03-25 21
  ```
  -- 显示 `Posted on 25 Mar 2020`
  -- 鼠标 `Created: 25 Mar 2020 11:54:57`
  猜想可能是没识别<!--出/到/懂-->出更新时间
- 预留时间只写到天<!--天数-->
  e.g., 
  > ```markdown
  date: 
  updated: 2020-03-25
  ```
  -- 显示 `Posted on 25 Mar 2020`
  -- 鼠标 `Created: 25 Mar 2020 11:59:52 / Modified: 00:00:00`
- 预留时间删掉 `date:` 
  e.g., 
  > ```markdown
  updated: 2020-03-25
  ```
  -- 显示 `Posted on 25 Mar 2020`
  -- 鼠标 `Created: 25 Mar 2020 12:02:57 / Modified: 00:00:00`
- 会报错，错误日志日志如下所示
  e.g., 
  > ```markdown
  <!--date:-->
  updated: 2020-03-25 21:
  ```
  - Error log
> ```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
ERROR Process failed: _posts/2020-03-25-Hexo-Troubles.md
YAMLException: incomplete explicit mapping pair; a key node is missed; or followed by a non-tabulated empty line at line 2, column 23:
    updated: 2020-03-25 21:
                          ^
    at generateError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:165:10)
    at throwError (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:171:9)
    at readBlockMapping (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1000:9)
    at composeNode (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1332:12)
    at readDocument (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1492:3)
    at loadDocuments (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1548:5)
    at Object.load (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/js-yaml/lib/js-yaml/loader.js:1569:19)
    at parseYAML (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:80:21)
    at parse (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-front-matter/lib/front_matter.js:56:12)
    at Promise.all.spread (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo/lib/plugins/processor/post.js:52:20)
    at tryCatcher (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:509:35)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:693:18)
    at Promise._fulfill (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:638:18)
    at PromiseArray._resolve (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:126:19)
    at PromiseArray._promiseFulfilled (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:144:14)
    at PromiseArray._iterate (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:114:31)
    at PromiseArray.init [as _init] (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise_array.js:78:10)
    at Promise._settlePromise (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:566:21)
    at Promise._settlePromise0 (/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/bluebird/js/release/promise.js:614:10)
INFO  Files loaded in 2.55 s
INFO  0 files generated in 10 s
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```


## Questions? (with Error log)


# Blogs (Markdown)

## 表格和文字颜色/背景色

文字颜色:  
Size 可选项包括数字 1-7，浏览器默认 3.  
个人猜测这种可选数目设置可能是对照了 markdown \# 小标题的字号可能性
```markdown
<font face="微软雅黑">微软雅黑</font>
<font color=grey size=7>颜色</font>
<table><tr><td bgcolor=orange>橙黄</td></tr></table>
```

文字背景色 / 表格底色:
```markdown
<span style="background-color: #FFF68F; font-weight: bold;">&nbsp; For example &nbsp;</span>
<table><td bgcolor=#C1FFC1 style="line-height: 1em">For example</td></table>
```

&sect;*** 示例:*** Font
- **Windows** &para;<br>  
<font face="Microsoft YaHei">Font: Microsoft YaHei</font>
<font face="Times New Roman">Font: Times New Roman</font>
<font face="Arial">  Font: Arial</font>
<font face="Tahoma"> Font: Tohoma</font>
<font face="Verdana">Font: Verdana</font>
<font face="SimSun"> Font: SimSun </font>
- **Mac OS, iOS** &para;<br>  
<font face="STHeiti">Font: STHeiti</font>
<font face="STXihei">Font: STXihei</font>
<font face="Heiti SC">Font: Heiti SC</font>
<font face="Hiragino Sans GB">Font: Hiragino Sans GB</font>
<font face="Helvetica">Font: Helvetica</font>
<font face="Helvetica Neue">Font: Helvetica Neue</font>
<font face="PingFang SC">Font: PingFang SC</font>
<font face="San Francisco">Font: San Francisco</font>
- **Android** &para;<br>  
<font face="Droid Sans">Font: Droid Sans</font>
<font face="Droid Sans Fallback">Font: Droid Sans Fallback</font>

**Helpful:**  
定义和用法: `<font>` 规定文本的字体、字体尺寸、字体颜色。  
[如何优雅的选择字体(font-family)](https://segmentfault.com/a/1190000006110417)  
[Markdown中如何添加特殊符号](https://blog.csdn.net/Logicr/article/details/82414854)  

**聊作参考**:
[\[workingNotes\]使用html5画实心圆的两种方法](https://blog.csdn.net/binglingxueyou/article/details/50778373)  
[HTML `<font>` 标签](https://www.w3school.com.cn/tags/tag_font.asp)  
[HTML和CSS中如何设置中文字体](https://blog.csdn.net/ght886/article/details/79222280)  
[CSS3 字体, RUNOOB.COM 菜鸟](https://www.runoob.com/css3/css3-fonts.html)  
[CSS 字体, RUNOOB.COM 菜鸟](https://www.runoob.com/css/css-font.html)  


## 列表 标识改变

markdown 语法的无序列表:  
这三种写法的外在表现形式都是一样的，即空心原点
```markdown
* Item
+ Item
- Item
```

html 写法:  
注意如果想改变列表标识，那么不能用无序列表 `<ul>` <!--，这个没用-->，必须用有序列表 `<ol>` ，否则改变 `list-style-type` 无用。如
```markdown
<ol style="list-style-type: square;"><li>Test</li></ol>
<ol style="list-style-type: disc;"><li>Test</li></ol>
```

注意 markdown 写法中，其实 `-- item` 是不会作为一种无序列表来展示的，只是作为普通文字内容显示出来，只不过由于 `--` 会自动缩成一个较 `-` 长一些的横而已，同理 `--- item` 亦然。所以以它俩作为起始，后面的文字不会有悬挂缩进效果。  
至于 `-`, `--`, `---` 的区别是：分别作为英文中的 连字符、连接号、和破折号来使用。

<!--
`list-style-type` 常见可选
- `none` 不使用项目符号
- `disc` 实心圆，默认值
- `circle` 空心圆
- `square` 实心方块
- `decimal` 阿拉伯数字
- `lower-roman` 小写罗马数字
- `upper-roman` 大写罗马数字
- `lower-alpha` 小写英文字母
- `upper-alpha` 大写英文字母

<ol style="list-style-type: lower-hexadecimal;"><li>Test</li></ol>
<ol style="list-style-type: lower-norwegian;"><li>Test</li></ol>

示例
<ol style="line-height: 1em; list-style-type: square;"><li> Test: square</li></ol>
<ol style="line-height: 1em; list-style-type: disc;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: circle;"><li> Test</li></ol>
<ol style="line-height: 1em; list-style-type: decimal;"><li>Test</li></ol>
<ol style="line-height: 1em; list-style-type: none;"><li>   Test</li></ol>

<ol style="line-height: 1em; list-style-type: lower-alpha;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: lower-armenian;"><li>Test</li></ol>
<ol style="line-height: 1em; list-style-type: lower-greek;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: lower-latin;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: lower-roman;"><li>   Test</li></ol>

<ol style="line-height: 1em; list-style-type: upper-alpha;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: upper-armenian;"><li>Test</li></ol>
<ol style="line-height: 1em; list-style-type: upper-latin;"><li>   Test</li></ol>
<ol style="line-height: 1em; list-style-type: upper-roman;"><li>   Test</li></ol>
-->

`list-style-type` 常见可选 *示例* 
<ol style="line-height: 1.7ex">
  <li style="list-style-type: square;"> square 实心方块</li>
  <li style="list-style-type: disc;">   disc 实心圆，默认值</li>
  <li style="list-style-type: circle;"> circle 空心圆</li>
  <li style="list-style-type: decimal;">decimal 阿拉伯数字 </li>
  <li style="list-style-type: none;">   none 不使用项目符号</li>

  <li style="list-style-type: lower-alpha;">   lower-alpha 小写英文字母</li>
  <li style="list-style-type: lower-armenian;">lower-armenian</li>
  <li style="list-style-type: lower-greek;">   lower-greek</li>
  <li style="list-style-type: lower-latin;">   lower-latin</li>
  <li style="list-style-type: lower-roman;">   lower-roman 小写罗马数字</li>

  <li style="list-style-type: upper-alpha;">   upper-alpha 大写英文字母  </li>
  <li style="list-style-type: upper-armenian;">upper-armenian</li>
  <li style="list-style-type: upper-latin;">   upper-latin   </li>
  <li style="list-style-type: upper-roman;">   upper-roman 大写罗马数字  </li>
</ol>

```markdown
<ol style="line-height: 1ex"> <!--2ex-->
  <li style="list-style-type: square;"> square </li>
  <li style="list-style-type: disc;">   disc   </li>
  <li style="list-style-type: circle;"> circle </li>
  <li style="list-style-type: decimal;">decimal</li>
  <li style="list-style-type: none;">   none   </li>

  <li style="list-style-type: lower-alpha;">   lower-alpha   </li>
  <li style="list-style-type: lower-armenian;">lower-armenian</li>
  <li style="list-style-type: lower-greek;">   lower-greek   </li>
  <li style="list-style-type: lower-latin;">   lower-latin   </li>
  <li style="list-style-type: lower-roman;">   lower-roman   </li>

  <li style="list-style-type: upper-alpha;">   upper-alpha   </li>
  <li style="list-style-type: upper-armenian;">upper-armenian</li>
  <li style="list-style-type: upper-latin;">   upper-latin   </li>
  <li style="list-style-type: upper-roman;">   upper-roman   </li>
</ol>
```


**Useful:**  
[Markdown: 列表](http://xianbai.me/learn-md/article/syntax/lists.html)  
[markdown基础入门——有序列表与无序列表](https://blog.csdn.net/qq_37590544/article/details/86602472)  
[HTML 去除li前面的小黑点,和ul、LI部分属性](https://blog.csdn.net/cqkxzyi/article/details/7606181)  

**不算太有用, 仅做参考**  
[HTML 列表, W3school](https://www.w3school.com.cn/html/html_lists.asp)  
[HTML `<ul>` 标签](https://www.w3school.com.cn/tags/tag_ul.asp)  
[在markdown中通过html语法实现表格中的有序列表和无需列表](https://blog.csdn.net/wiborgite/article/details/79456107)  
[CSDN Markdown 你需要掌握的小方法](https://blog.csdn.net/soledadzz/article/details/52933606)  

## `-`, `--`, and `---`

[英文破折号 (em dash)、连接号 (en dash) 与连字符 (hyphen) 的区别及各自用法是什么? 在科技写作中有何特点?](https://www.zhihu.com/question/20332423)  
[magasa 的回答 - 知乎](https://www.zhihu.com/question/20332423/answer/15367631)  

1. &diams;&nbsp;&nbsp; `-`, 连字符 (hyphen):
    1. 用于复合词，如 `upper-case letter`
    2. 用于分隔数字或字母，例如电话号码，或是名字的拼写
    > `1-800-621-2376`
    > `My name is Phyllis; that's p-h-y-l-l-i-s.`
    3. 用于排版时连接因断行而被打断的单词，如
    > `Trust Law ranks the Congo as one of the most dangerous coun-`
    > `tries for sexual violence.`
2. &diams;&nbsp;&nbsp; `--`, 连接号 (en dash):
    1. 相当于 to. 主要用于连接数字或单词，表示 "到并包括" (up to and including). 
    需要注意的是，在 from...to... 和 between...and... 结构中，不要用 en dash 去替代中间的 to 和 and.
    > Her college years, 1998--2002, were the happiest in her life.
    > For documentation and indexing, see chapters 16--18.
    > In Genesis 6:13--22 we find God's instructions to Noah.
    > Join us on Thursday, 11:30 a.m.--4:00 p.m., to celebrate the New Year.
    > The London--Paris train leaves at two o'clock.
    > I have blocked out December 2002--March 2003 to complete my manuscript.
    > Her articles appeared in Postwar Journal (3 November 1945--4 February 1946).
    > Green Bay beat Denver 31--24.The legislature voted 101--13 to adopt the resolution.
    2. 后面什么也不接。比如用于表示年代，若时间仍在进行中，en dash 后不要加空格。
    > Professor Plato's survey (1999--) will cover the subject in the final volume.
    > Jane Doe (1950--); or Jane Doe (b. 1950)
    3. 代替 hyphen 的用途。在复合型形容词中，如果其中一个构成元素是开放型复合词，或者如果其中两个或多个构成元素是开放型复合词或带 hyphen 的复合词，那么应使用 en dash。
    4. 其他用法：en dash 有时用作减号，尽管两者原则上并非同一个符号。另外，它也可以用于连接拥有不同校区的大学。
3. &diams;&nbsp;&nbsp; `---`, 破折号 (em dash):
    1. 它的用法最复杂、最灵活。为了避免混淆，一个句子不应包含超过两个 em dash，如果实在需要，应使用圆括弧。
    2. 用于详述或解释。基本相当于一组逗号、圆括弧，或冒号的用途。
    3. 用于分隔引导从句的代词。
    4. 表示思考或对话中句子结构的突然中断，有时也可用省略号代替。
    但如果中断来自于所引用材料的外部，em dash 应当出现在引号的外面。
    5. 替代逗号，或与逗号一起使用。如果在需要使用 em dash 时，需要用逗号来分隔从句和独立分句时，逗号可以省略。
    但如果 em dash 出现在引用材料的末尾表示中断，应当在说话人的身份之前用逗号。
    6. 和其他标点连用。一般来说，em dash 可以跟在问号、感叹号的后面，但不能跟在逗号、冒号、分号的后面，也几乎不能跟在句号的后面。
    7. 用于代替引号。有些法语作家常用 em dash 代替引号表示对话，每段话另起一段。
    8. 用于索引。

在科学论文中，这几种标点的使用有什么特殊之处呢？  
一般性的使用，如连接复合词、数字、年代等，和上面介绍的普通用法一致，但有两点或许需要特别注意。  
1. &spades;&nbsp;&nbsp; 慎用 en dash
  为了避免和减号混淆，有的地方最好不要用 en dash。例句：
  > with temperature of −5 to 25°C 【正确】
  > with temperature of −5--25°C 【错误】
  > −4 to −6°C 【正确】
  > −4-- −6°C 【错误】
2. &clubs;&nbsp;&nbsp; 少用 em dash
  有一部分科技论文写作参考书，例如 *Mastering Scientific and Medical Writing: A Self-help Guide*，认为在科技论文中三种 em dash 一律不应采用，em dash 经常表示一种强有力的打断，如果可能，最好用更平滑、更柔和的圆括弧替代。
  权威的 *Scientific Style and Format: The CBE Manual for Authors, Editors, and Publishers* 也不推荐在参考文献中使用 3-em dash 来表示相同作者这一格式。

## 列表: 倒序, 序号起始点
有序列表的序号可以自行设置起始点，而非从默认值 1 开始；也可以倒序展示。

语法 (其中若写成 `reversed="1"` 也是一样的效果)
```markdown
<ol style="line-height: 1ex; list-style-type: lower-roman;" reversed="0">
    <li>Part I
        <ol style="list-style-type: decimal;" start="3">
            <li>Item 1</li>
            <li>Item 2</li>
        </ol>
    </li>
    <li>Part II
        <ol style="list-style-type: decimal;" start="7">
            <li>Item 3</li>
            <li>Item 4</li>
        </ol>
    </li>
</ol>
```
展示效果
<ol style="line-height: 1ex; list-style-type: lower-roman;" reversed="0">
    <li>Part I
        <ol style="list-style-type: decimal;" start="3">
            <li>Item 1</li>
            <li>Item 2</li>
        </ol>
    </li>
    <li>Part II
        <ol style="list-style-type: decimal;" start="7">
            <li>Item 3</li>
            <li>Item 4</li>
        </ol>
    </li>
</ol>

ol 序号不重新开始  
[ol 有序列表序号的倒序](http://note.rpsh.net/posts/2011/12/27/reverse-ordered-lists-in-html5/)  
[ol 腾讯云](https://cloud.tencent.com/developer/section/1189739)  
[HTML \<ol\> 元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ol)  
[关于css中为什么ol标签不显示序号的解决办法](https://blog.csdn.net/FJ2010080080026/article/details/38581173)  


## Md 部分语法 (超链接, 锚点, 任务列表)
<!--## Markdown 语法-->

### 超链接

**行内式**
```markdown
[打开百度](http://www.baidu.com)
[打开百度](http://www.baidu.com "打开百度")
```
说明: [] 里写链接文字，() 里写链接地址, () 中的 "" 中可以为链接指定 title 属性，title 属性可加可不加。title 属性的效果是鼠标悬停在链接上会出现指定的 title 文字。[链接文字](链接地址 “链接标题”) 这样的形式。链接地址与链接标题前有一个空格。

**参考式**
参考式超链接一般用在学术论文上面，或者另一种情况，如果某一个链接在文章中多处使用，那么使用引用的方式创建链接将非常好，它可以让你对链接进行统一的管理。
```markdown
[1]:http://www.google.com "google"
[2]:http://www.baidu.com "Baidu"
[3]:http://www.51cto.com "51cto"
[4]:http://www.aiqiyi.com "aiqiyi"
[网站]:http://www.qq.com
我经常浏览的几个网站[Google][1]、[Baidu][2]、[51CTO][3]和看视频的网站[爱奇艺][4]感觉都是很不错的[网站][]. 
特别是我常用的 Gmail, Google Calendar 都需要[它的存在][1].
```

[1]:http://www.google.com "google"
[2]:http://www.baidu.com "Baidu"
[3]:http://www.51cto.com "51cto"
[4]:http://www.aiqiyi.com "aiqiyi"
[网站]:http://www.qq.com
我经常浏览的几个网站[Google][1]、[Baidu][2]、[51CTO][3]和看视频的网站[爱奇艺][4]感觉都是很不错的[网站][]. 
特别是我常用的 Gmail, Google Calendar 都需要[它的存在][1].

注意定义链接内容应该在引用链接之前。如代码块中的写法 work, 但其后的写法就不行。

**自动链接**
```markdown
<http://www.baidu.com/>
<admin@baidu.com>
```
说明：Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用<>包起来， Markdown 就会自动把它转成链接。一般网址的链接文字就和链接地址一样。

<http://www.baidu.com/>
<admin@baidu.com>

### \*参考式 超链接
ref: [Markdown 超链接](http://xianbai.me/learn-md/article/syntax/links.html)  
参考式链接的写法相当于行内式拆分成两部分，并通过一个 识别符 来连接两部分。参考式能尽量保持文章结构的简单，也方便统一管理 URL。  
1. 首先定义链接，`[Google][link]`
  其中第二个方括号内为识别符，每个链接的识别符应是独有的，可以是字母、数字、空白或者是标点符号，不区分大小写
2. 然后定义链接内容，`[link]: https://www.google.com/` "Google"
  链接内容的定义最好放在引用链接前面
3. 也可以省略识别符，使用链接文本作为识别符
  猜测：同一个文件里只能省略一次
```markdown
[Google][]
[Google]: http://www.google.com/ "Google"
```
参考式相对于行内式有一个明显的优点，就是可以在多个不同的位置引用同一个 URL。

e.g., 
[Google]:http://www.google.com "google"
[Baidu]:http://www.baidu.com "Baidu"
[51CTO]:http://www.51cto.com "51cto"
[4]:http://www.aiqiyi.com "aiqiyi"
[网站]:http://www.qq.com
我经常浏览的几个网站[Google][]、[Baidu][]、[51CTO][]和看视频的网站[爱奇艺][4]感觉都是很不错的[网站][]. 
特别是我常用的 Gmail, Google Calendar 都需要[它的存在][1].
```markdown
:http://www.google.com "google"
[Baidu]:http://www.baidu.com "Baidu"
[51CTO]:http://www.51cto.com "51cto"
[4]:http://www.aiqiyi.com "aiqiyi"
[网站]:http://www.qq.com
我经常浏览的几个网站[Google][]、[Baidu][]、[51CTO][]和看视频的网站[爱奇艺][4]感觉都是很不错的[网站][]. 
特别是我常用的 Gmail, Google Calendar 都需要[它的存在][1].
```

### 锚点

网页中，锚点其实就是页内超链接，也就是链接本文档内部的某些元素，实现当前页面中的跳转。比如这里写下一个锚点，点击回到目录，就能跳转到目录。   在目录中点击这一节，就能跳过来。还有下一节的注脚。这些根本上都是用锚点来实现的。  
注意：Markdown Extra 只支持在标题后插入锚点，其它地方无效

**1, 页内超链接:**
```markdown
# 1.分级目录{\#index}
  跳转到[标题]{\#index}
```
说明：在你准备跳转到的指定标题后插入锚点 `{\#标记}`，然后在文档的其它地方写上连接到锚点的链接。此处使用的是 GitHub 风格的 Markdown 语法所以无法正常显示效果，推荐使用以下 `2, 文章内部标题链接`。

**2, 文章内部标题链接:**  
```markdown
* [目录1](#40)
   * [标题1](#41)
   * [标题2](#42)
   * [标题3](#43)
   * [标题4](#44)

<h3 id="41">标题1</h3>
    轻轻的我走了， 正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
<h3 id="42">标题2</h3>
    正如我轻轻的来； 我轻轻的招手， 作别西天的云彩。
<h3 id="43">标题3</h3>
    我轻轻的招手， 作别西天的云彩。
<h3 id="44">标题4</h3>
    作别西天的云彩。
```

### 列表: 任务列表
要创建任务列表，前缀列表项[ ]。要将任务标记为完整，请使用[x]

语法
```markdown
- [ ] 跑步
- [ ] 骑车
- [x] 吃饭
- [ ] 睡觉
```
展示效果
- [ ] 跑步
- [ ] 骑车
- [x] 吃饭
- [ ] 睡觉

## 多图模式

```markdown
{% gp r-c %}
<img src=""> x n
{% endgp %}
```

| n | r-c | result |
|---|-----|--------|
| 2 | 1-2 | 2 |
| 3 | 1-3 | 3 |
| 4 | 4-3 | 2,2 |
| 5 | 5-3 | 2,3 |
| 5 | 5-2 | 2,1,2 |
| 5 | 8-7 | 3,2 |
| 7 | 8-5 | 2,3,2 |

若是一张图，就使用 `<img src="" width="?%">` 即可。  
`?%` 可为 1-100 间任意值，代表整个网页宽度的百分比。

若是连续几张图，比如说两张，  
下面这两种写法展示出来虽然都是分两行展示，但是间隙略有不同：  
第一种两张图中间紧挨着，几乎没有缝隙；  
第二种空隙更大，仿佛就是分了两行。  
其中 `?%` 仍然同上，不非得是 `width="100%"` 
```markdown
# Method 1
<img src="" width="?%"><img src="" width="?%">

# Method 2
<img src="" width="?%">
<img src="" width="?%">
```


## Q & A

# Git & GitHub

## "ca-certificates" & "RPC failed; curl"

第一个是 ssh 验证问题，我在 Ubuntu Firefox 中尝试打开 github，也提示了连接问题（现在又好了，浏览器可以进），所以可能是那会就是连不上？  
第二个按照网上的方法并没解决，其中一个是 ·git config xxx number· ，后来我又把文件都加回来（上一个 push 是试图删掉一些文件的），即压缩后的图片，又可以正常 push 了。所以难道是删除文件不行？

*Used:*
`git config http.sslverify false`
`git config http.postBuffer 1048576000`


fatal: unable to access : server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none  
[git错误error: server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none](https://www.jianshu.com/p/7d599bdf370a)  
[Git: client error, server certificate verification failed](https://fabianlee.org/2019/01/28/git-client-error-server-certificate-verification-failed/)  
[\[SOLVED\] "server certificate verification failed"](https://bbs.archlinux.org/viewtopic.php?id=251096)  
[Server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none](https://github.com/NVIDIA/nvidia-docker/issues/813)  
[错误：server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none](https://blog.csdn.net/liurizhou/article/details/91361223)  
[server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none](https://stackoverflow.com/questions/21181231/server-certificate-verification-failed-cafile-etc-ssl-certs-ca-certificates-c)  

error: RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.  
[git error: RPC failed; curl 56 GnuTLS](https://stackoverflow.com/questions/38378914/git-error-rpc-failed-curl-56-gnutls)  
[\[Solution\] gnutls_handshake() failed GIT repository – AWS codecommit](https://devopscube.com/gnutls-handshake-failed-aws-codecommit/)  
[error: RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.](https://blog.csdn.net/ai2000ai/article/details/80708079)  

您必须在 sources.list 中指定代码源(deb-src) URI  
[E: 您必须在 sources.list 中指定代码源(deb-src) URI 解决办法](https://blog.csdn.net/weixin_38634889/article/details/97941817)  
[Ubuntu下安装gcc报错：E: 您必须在 sources.list 中指定代码源(deb-src) URI](https://www.cnblogs.com/51ma/p/12033773.html)  
[E: 您必须在 sources.list 中指定代码源(deb-src) URI 解决办法](https://blog.csdn.net/Zhanganliu/article/details/86592524)  


### server certificate verification failed. CAfile
fatal: unable to access : server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date -s
date：选项需要一个参数 -- s
Try 'date --help' for more information.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date --s
date：选项 ‘--set’ 需要一个参数
Try 'date --help' for more information.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date --help
用法：date [选项]... [+格式]
　或：date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
Display the current time in the given FORMAT, or set the system date.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date
Thu Mar 26 18:09:05 CDT 2020



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ sudo apt-get install apt-transport-https ca-certificates -y
[sudo] ubuntu 的密码： 
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
下列软件包是自动安装的并且现在不需要了：
  linux-headers-4.15.0-47 linux-headers-4.15.0-47-generic
  linux-headers-4.15.0-50 linux-headers-4.15.0-50-generic
  linux-headers-4.15.0-51 linux-headers-4.15.0-51-generic
  linux-headers-4.15.0-52 linux-headers-4.15.0-52-generic
  linux-headers-4.15.0-54 linux-headers-4.15.0-54-generic
  linux-headers-4.15.0-55 linux-headers-4.15.0-55-generic
  linux-image-4.15.0-47-generic linux-image-4.15.0-50-generic
  linux-image-4.15.0-51-generic linux-image-4.15.0-52-generic
  linux-image-4.15.0-54-generic linux-image-4.15.0-55-generic
  linux-modules-4.15.0-47-generic linux-modules-4.15.0-50-generic
  linux-modules-4.15.0-51-generic linux-modules-4.15.0-52-generic
  linux-modules-4.15.0-54-generic linux-modules-4.15.0-55-generic
  linux-modules-extra-4.15.0-47-generic linux-modules-extra-4.15.0-50-generic
  linux-modules-extra-4.15.0-51-generic linux-modules-extra-4.15.0-52-generic
  linux-modules-extra-4.15.0-54-generic linux-modules-extra-4.15.0-55-generic
使用'sudo apt autoremove'来卸载它(它们)。
下列软件包将被升级：
  apt-transport-https ca-certificates
升级了 2 个软件包，新安装了 0 个软件包，要卸载 0 个软件包，有 159 个软件包未被升级。
需要下载 194 kB 的归档。
解压缩后会消耗 0 B 的额外空间。
获取:1 https://mirrors.tuna.tsinghua.edu.cn/ubuntu xenial-updates/main amd64 apt-transport-https amd64 1.2.32 [26.5 kB]
获取:2 https://mirrors.tuna.tsinghua.edu.cn/ubuntu xenial-updates/main amd64 ca-certificates all 20170717~16.04.2 [167 kB]
已下载 194 kB，耗时 0秒 (233 kB/s)   
正在预设定软件包 ...
(正在读取数据库 ... 系统当前共安装有 520023 个文件和目录。)
正准备解包 .../apt-transport-https_1.2.32_amd64.deb  ...
正在将 apt-transport-https (1.2.32) 解包到 (1.2.29ubuntu0.1) 上 ...
正准备解包 .../ca-certificates_20170717~16.04.2_all.deb  ...
正在将 ca-certificates (20170717~16.04.2) 解包到 (20170717~16.04.1) 上 ...
正在处理用于 man-db (2.7.5-1) 的触发器 ...
正在设置 apt-transport-https (1.2.32) ...
正在设置 ca-certificates (20170717~16.04.2) ...
正在处理用于 ca-certificates (20170717~16.04.2) 的触发器 ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ sudo update-ca-certificates
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date
Thu Mar 26 18:12:27 CDT 2020
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ openssl s_client -showcerts -servername git.mycompany.com -connect git.mycompany.com:443 </dev/null 2>/dev/null | sed -n -e '/BEGIN\ CERTIFICATE/,/END\ CERTIFICATE/ p'  > git-mycompany-com.pem
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ date
Thu Mar 26 18:14:32 CDT 2020
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config
用法：git config [<选项>]
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config http.sslverify
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config http.sslverify --get
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git config http.sslverify false
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
```

### RPC failed; curl 56 GnuTLS recv error (-54)
RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
Username for 'https://github.com': eustomaqua
Password for 'https://eustomaqua@github.com': 
对象计数中: 67, 完成.
Delta compression using up to 2 threads.
压缩对象中: 100% (67/67), 完成.
写入对象中: 100% (67/67), 933.08 KiB | 0 bytes/s, 完成.
Total 67 (delta 24), reused 0 (delta 0)
error: RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 


ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

    git-mycompany-com.pem

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ whereis git-mycompany-com.pem
git-mycompany-com:
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 



ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git push
Username for 'https://github.com': eustomaqua
Password for 'https://eustomaqua@github.com': 
对象计数中: 67, 完成.
Delta compression using up to 2 threads.
压缩对象中: 100% (67/67), 完成.
写入对象中: 100% (67/67), 933.08 KiB | 0 bytes/s, 完成.
Total 67 (delta 24), reused 0 (delta 0)
error: RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io$ 
```

## FAQ

# \*References

**Helpful:**  
[Markdown 语法整理](https://guo365.github.io/study/Markdown.html#11)  
[Markdown 书写风格指南](https://einverne.github.io/markdown-style-guide/zh.html)  

