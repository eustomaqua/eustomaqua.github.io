---
title: Hexo+NexT, Trouble Solver
date: 2020-03-27 14:59:15
updated: 2020-03-25 21:36:22
categories:
  - Records
tags:
  - Hexo
  - Debug
  - LaTeX
  - Markdown
  - Git
mathjax: true
---



<!--
date: 2020-03-25 03:53:56
updated: 2020-03-25 21:36

SHOW:
Post on __25 Mar 2020
Created 25 Mar 2020 09:21:22 / Modified: 21:36:00

updated: 2020-03-25 21:36:22

Created: 27 Mar 2020 14:59:15
Modified: 25 Mar 2020 21:36:22 CDT
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
~/eustomaqua.github.io/hexo-next$ hexo clean
INFO  Deleted database.
INFO  Deleted public folder.
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
```
#### YAMLException: imcomplete explicit mapping pair
```bash
~/eustomaqua.github.io/hexo-next$ hexo clean
INFO  Deleted database.
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
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
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
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
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
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
~/eustomaqua.github.io/hexo-next$ hexo s
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
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
```


## lastIndex of undefined

简记出问题的文件为 `bug.md`
1. 寻找占用端口 4000 的程序并杀掉，但是好像没有占用的。另外这个命令需 root 权限
  ```bash
  $ su
  # netstat -tunlp | grep 4000
  # kill -9 [process-id]
  # exit
  ```
  此处记录另外两个命令，但是这里没有尝试
  ```bash
  $ ps -ef | grep 4000
  $ lsof -i:4000
  ```
2. 尝试逐块重新复制进来，发现 hexo g 正常。但是 hexo s 会提示端口被占用，也就是最开始出现的错误情形。此时再继续尝试 hexo g 就会报错。两个错误提示可见下列的两个 log  
  另外有网友说是代码块没有指定语言的问题，这个好像也没有找到。 ref: [运行`hexo g`出错 \#1913](https://github.com/hexojs/hexo/issues/1913)
3. 把错误文件移除，尝试 hexo g, hexo s 可以正常生成网页。此时再把 `bug.md` 移入，即可正常执行。

<!--2020-04-12 3:28am 移除--> 
**备注：** 这个错误还出现过一次，当时情景是我修改了标签云的颜色，其他 .md 文件基本都没改（只给 2018 年 hexo 文件的标签云部分加粗了两个关键词）。 纠正过程是先把所有 .md 文件都移出 source/\_posts 文件夹，然后再逐个移回：2018 年 5 篇；2019 年 5 篇；2020 年 6 篇；2020 年 2 篇；2020 年 latex badge ；2020 年 hexo troubles 。移动过程中逐个生成 hexo g 均正常，最后移动完成后就没有再出现此问题了

查看 使用端口的程序  
[linux 下查看进程占用端口和端口号占用进程命令](https://blog.csdn.net/gochenguowei/article/details/80926000)  
[linux下查看某一端口被哪个进程占用](https://blog.csdn.net/xiangwanpeng/article/details/78804225)  
*here:* http://hexo.io/docs/troubleshooting.html *Error: listen EADDRINUSE 0.0.0.0:4000*  
[hexo搭建博客过程中出现的问题，4000端口被占用](https://segmentfault.com/q/1010000008546859)  
[Hexo--hexo server失败，提示端口被占用](https://www.difashi.com/2019-08/17-hexo-2.html)  

TypeError: Cannot set property 'lastIndex' of undefined  
[运行`hexo g`出错 \#1913](https://github.com/hexojs/hexo/issues/1913)  
[TypeError: Cannot set property 'lastIndex' of undefined](https://github.com/hexojs/hexo/issues/2380)  

```bash
# hexo-g  # work normally

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

```bash
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
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

## 谨慎使用大括号(花括号)

Code causing error:
```markdown
[关于 hexo 对文章渲染解析{{}}的问题](https://www.v2ex.com/t/510207)  
[关于 hexo 对文章渲染解析\{\{\}\}的问题](https://www.v2ex.com/t/510207)  
[关于 hexo 对文章渲染解析``{{}}``的问题](https://www.v2ex.com/t/510207)  
```

Solve: 删掉这两对花括号/大括号即可。

Error log
```shell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ hexo g
INFO  Start processing
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 554, Column 154]
  unexpected token: }}
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
~/eustomaqua.github.io/hexo-next$ hexo g
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
~/eustomaqua.github.io/hexo-next$ 
```

## 网站底部字数统计

[HEXO\_网站底部字数统计](http://www.wenxin.wiki/2018/11/22/HEXO-%E7%BD%91%E7%AB%99%E5%BA%95%E9%83%A8%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1/)  
[Hexo 搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)  

### Attempt 1: Failed

1. 安装插件，切换到根目录
  (早在搭建博客时已安装，详见 {% post_link 2018-07-14-Hexo-NexT Build_up_your_website %} )
  ```bash
  $ npm install hexo-wordcount --save
  ```

2. 找到 `/themes/next/layout/_partials/footer.swig` 文件， 
  第 42--52 行内的最后加上如下第 12--15 行代码
  ```html
{% if theme.footer.counter %}
  <script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
  <span class="post-meta-divider">|</span>
  <span id="busuanzi_container_site_pv">
    Total visits<span id="busuanzi_value_site_pv"></span>
  </span>
  <span class="post-meta-divider">|</span>
  <span id="busuanzi_container_site_uv">
    Total visitors<span id="busuanzi_value_site_uv"></span>
  </span>
  <span class="post-count">|</span>
  <span>
    Total count: {{ totalcount(site) }} words
  </span>
{% endif %}
  ```

### Attempt 2: Not as expected

1. 在根目录下执行如下命令安装相关依赖
```bash
$ npm install hexo-symbols-count-time --save
```
  启动该功能需要同时修改站点配置文件和主题配置文件。
```bash
~/eustomaqua.github.io/hexo-next$ npm install hexo-symbols-count-time --save
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.4 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.4: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

+ hexo-symbols-count-time@0.7.1
added 31 packages from 289 contributors and audited 3611 packages in 100.142s
found 195 vulnerabilities (136 low, 5 moderate, 54 high)
  run `npm audit fix` to fix them, or `npm audit` for details
~/eustomaqua.github.io/hexo-next$ 


~/eustomaqua.github.io/hexo-next$ npm audit fix
npm WARN checkPermissions Missing write access to /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/nunjucks/node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

npm ERR! path /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access
npm ERR! Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string'
npm ERR!  { [Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string']
npm ERR!   cause:
npm ERR!    { Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string'
npm ERR!      errno: -13,
npm ERR!      code: 'EACCES',
npm ERR!      syscall: 'access',
npm ERR!      path:
npm ERR!       '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string' },
npm ERR!   isOperational: true,
npm ERR!   stack:
npm ERR!    'Error: EACCES: permission denied, access \'/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string\'',
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path:
npm ERR!    '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string' }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator (though this is not recommended).

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/ubuntu/.npm/_logs/2020-03-27T12_17_55_906Z-debug.log
~/eustomaqua.github.io/hexo-next$ 
```

2. 在 *站点配置文件* `./_config.yml` 中添加配置项，用于控制每项统计信息是否显示。
```yaml
symbols_count_time:
  symbols: true # 统计单篇文章字数
  time: false # 取消估算单篇文章阅读时间
  total_symbols: true # 统计站点总字数
  total_time: false # 取消估算站点总阅读时间
```

3. 在 *主题配置文件* `themes/next/_config.yml` 中做如下修改，用于控制统计信息的显示样式。
```yaml
symbols_count_time:
  separated_meta: false # 统计信息不换行显示
  item_text_post: true # 文章统计信息中是否显示“本文字数/阅读时长”等描述文字
  item_text_total: true # 站点统计信息中是否显示“本文字数/阅读时长”等描述文字
  awl: 4 # Average Word Length：平均字符长度
  wpm: 275 # Words Per Minute：阅读速度
```
  汉字的平均字符长度为 1.5 ，如果在文章中使用纯中文进行写作（没有混杂英文），那么推荐设置 `awl: 2` 及 `wpm: 300`，但是如果文章中存在英文，建议设置 `awl: 4` 及 `wpm: 275`。

4. 因为修改了站点配置文件，所以需要重新启动服务器才能生效。


### Attempt 3: Work

1. 卸载模块 hexo-symbols-count-time
```bash
~/eustomaqua.github.io/hexo-next$ npm uninstall hexo-symbols-count-time -g
up to date in 0.076s

~/eustomaqua.github.io/hexo-next$ npm uninstall hexo-symbols-count-time -g
up to date in 0.051s
~/eustomaqua.github.io/hexo-next$ npm uninstall hexo-symbols-count-time
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.4 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.4: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

removed 31 packages and audited 3570 packages in 7.567s
found 195 vulnerabilities (136 low, 5 moderate, 54 high)
  run `npm audit fix` to fix them, or `npm audit` for details
~/eustomaqua.github.io/hexo-next$ npm audit fix
npm WARN checkPermissions Missing write access to /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules/nunjucks/node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.0.0 (node_modules/chokidar/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.12: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

npm ERR! path /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access
npm ERR! Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string'
npm ERR!  { [Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string']
npm ERR!   cause:
npm ERR!    { Error: EACCES: permission denied, access '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string'
npm ERR!      errno: -13,
npm ERR!      code: 'EACCES',
npm ERR!      syscall: 'access',
npm ERR!      path:
npm ERR!       '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string' },
npm ERR!   isOperational: true,
npm ERR!   stack:
npm ERR!    'Error: EACCES: permission denied, access \'/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string\'',
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path:
npm ERR!    '/home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/underscore.string' }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator (though this is not recommended).

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/ubuntu/.npm/_logs/2020-03-27T13_23_16_146Z-debug.log
~/eustomaqua.github.io/hexo-next$ 
```

2. 修改 `/themes/next/layout/_macro/post.swig` 文件，发现第 74 行的 `<div class="post-meta">` 已添加了相应代码，即第 281--292 行
```yaml
          {% if theme.word_count %}
            <span class="post-letters-count">
              &nbsp; | &nbsp;
              <span title="{{ __('post.wordcount') }}">
                {{ wordcount(post.content) }} words
              </span>
              &nbsp; | &nbsp;
              <span title="{{ __('post.min2read') }}">
                {{ min2read(post.content) }} minutes
              </span>
            </span>
          {% endif %}
```

3. 修改 `/themes/next/layout/_partials/footer.swig` 文件，在 `原 55--59 行的最前方` (not `原 42--52 行里的最后`) 添加下面代码块中语句
```yaml
  <div class="theme-info">
    <div class="powered-by-post-count"></div>
    <span class="post-count">共{{ totalcount(site) }}字</span>
  </div>
```
  修饰后第 55--64 行代码如下所示
  ```yaml
  <div class="total-wordcount-info">
    <div class="powered-by-post-count"></div>
    <span class="post-count">Total {{ totalcount(site) }} Words</span>
    <span class="post-meta-devider"> | </span>
  </div>
  ```
  或是在 `原 55 行之前` 加上
  ```yaml
{% if theme.footer.powered.enable and theme.footer.theme.enable %}
  <div class="total-wordcount-info">
    <div class="powered-by-post-count"></div>
    <span class="post-count">Total {{ totalcount(site) }} Words</span>
  </div>
  <span class="post-meta-devider">|</span>
{% endif %}
  ```

4. (3') 最后的代码修改为
```yaml
{% if theme.footer.powered.enable %}
  <div class="theme-info">
    <div class="powered-by-post-count"></div>
    <span class="post-count">Total {{ totalcount(site) }} Words</span>
  </div>
  <span class="post-meta-divider">|</span>
  <div class="powered-by">{#
  #}{{ __('footer.powered', '<a class="theme-link" target="_blank"' + nofollow + ' href="https://hexo.io">Hexo</a>') }}{% if theme.footer.powered.version %} v{{ hexo_env('version') }}{% endif %}{#
#}</div>
{% endif %}
```

hexo 全站总字数  
[为Hexo NexT主题添加字数统计功能](https://eason-yang.com/2016/11/05/add-word-count-to-hexo-next/)  
[hexo页脚添加访客人数和总访问量](https://www.jianshu.com/p/c311d31265e0)  
[Hexo-NexT魔改系列-03-添加数据统计](https://www.wqh4u.cn/2019/09/15/Hexo-NexT%E9%AD%94%E6%94%B9%E7%B3%BB%E5%88%97-03-%E6%B7%BB%E5%8A%A0%E6%95%B0%E6%8D%AE%E7%BB%9F%E8%AE%A1/)  
npm 删除插件  
[npm 安装卸载模块 & ionic插件安装与卸载](https://www.jianshu.com/p/5183053f2e95)  
[【npm】利用npm安装/删除/发布/更新/撤销发布包目录](https://www.cnblogs.com/penghuwan/p/6973702.html)  
[npm卸载模块](https://blog.csdn.net/qq_38543537/article/details/78522199)  
hexo powered by  
[Hexo 中如何才可去除底部的 Powered by 信息 ?](https://www.zhihu.com/question/47761889)  
[Hexo-Next底部powered by的logo栏更改以及注意事项（附官方文档,文末有福利链）](https://www.jianshu.com/p/4fbc57269f1b)  

## 站内文章自引

hexo 引用自己的博文  
[如何在Hexo的博文中引用自己的文章](https://www.mls-tech.info/hexo/hexo-use-internal-link/)  
[Hexo引用站内文章](https://www.jibing57.com/2017/10/30/how-to-use-post-link-on-hexo/)  

引用自己写的另一篇文章有两种方法。

- 使用标准 Markdown 引用语法，这种写法需要知道 Hexo 将博文转换后的命令规则，*如默认规则是 "/year/month/day/title" 即 "/年/月/日/文章名" ，而我修改成了 "/year/title"*。但是显然这种做法缺乏灵活性和可维护性。

- 也可以使用 Hexo 内置的标签语法来实现文章对内部博文的引用，语法如下：
```markdown
{% post_link 文件名(不要后缀) 文章别名(可选) %}
```
  其中文件名指的是博文的文件名，例如博客中有一篇文件名为 HelloWorld.md 的博客，就可以使用 ``{\% post_link HelloWorld \%}`` 来引用，Hexo 会自动将 HelloWorld 这篇博文的标题 (title) 显示在文章中，并带上正确的链接。 
  当然也可以给链接使用另外一个名字，比如 "MyHelloWorld我的"，就可以使用 ``{\% post_link HelloWorld MyHelloWorld我的 \%}``  
  如果博文在子目录中，也可以包含目录名。

**注意**:  
1. 文件名这一项是可以带上目录名的，比如若将 HelloWorld.md 文件放在了 `_post/hello` 这个目录下，那么引用时需要跟上目录名，否则会引用不到。
  ```markdown
  {% post_link hello/HelloWorld %}
  ```
2. 加入内部链接后，直接运行 `hexo server` 是看不到效果的，必须先运行 `hexo generate` 命令重新生成相关的博文才能看到链接。  


## 侧边栏邮箱链接

在站点配置文件 `./_config.yml` 中，
```yaml
social:
  E-Mail: mailto:your-email-address
```
也可以在主题配置文件 `./themes/next/_config.yml` 里修改，同样是搜索 `social` 可得。  

**注意** 侧边栏的图标，
- 我之前的写法是：
  ```yaml
social:
  GitHub: https://github.com/eustomaqua
  E-Mail: mailto:your-email-address
  ```
  这样写 GitHub 图标正常，但是 Email 是个小地球形状。
- 修改成如下写法：
  ```yaml
social:
  GitHub: https://github.com/eustomaqua
  E-Mail: mailto:your-email-address || envelope
  ```
  此时 Email 图标正常了，但是 GitHub 变成小地球的图片了。
- 继续修改：
  ```yaml
social:
  GitHub: https://github.com/eustomaqua || github
  E-Mail: mailto:your-email-address || envelope
  ```
  终于都正常了
  *猜测* 小地球图片应该是个默认选项，或者没有合适图标时出现

search: hexo 添加 email  
[Hexo - NexT - 在侧边栏添加邮箱](https://www.yanyunliang.com/2018/11/10/hexo-next-add-a-mailbox-to-the-sidebar.html)  
[请问怎么在侧边栏社交处添加邮箱呢](https://github.com/iissnan/hexo-theme-next/issues/1489)  
[Hexo博客Next主题个性设置集锦](http://www.mdslq.cn/archives/40609c5b.html#%E6%96%87%E7%AB%A0%E5%8A%A0%E5%AF%86%E8%AE%BF%E9%97%AE)  
[hexo博客设置自己的邮箱链接、及分类归档的设置](https://blog.csdn.net/qq_42893625/article/details/102671013)  

**Not Useful:**  
本想解决侧边栏图标和对应文字之间太紧密的问题，想添加个空格，没添加成。或许可能与主题有关。改变主题布局或可能行，不过我没尝试。  
*补充：* E-Mail 与图标之间的空格确实与主题布局有关，使用 `scheme: Gemini` 可达到想要的效果

hexo 侧边栏图标  
[hexo侧边栏社交小图标设置](https://www.jianshu.com/p/7e30afa09fab)  
[HEXO\_侧边栏社交小图标设置](http://www.wenxin.wiki/2018/11/22/HEXO-%E4%BE%A7%E8%BE%B9%E6%A0%8F%E7%A4%BE%E4%BA%A4%E5%B0%8F%E5%9B%BE%E6%A0%87%E8%AE%BE%E7%BD%AE/)  
hexo 侧边栏图标 空格  
[Hexo和NexT主题个性配置和优化](https://otuki.top/Hexo%E5%92%8CNexT%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E9%85%8D%E7%BD%AE%E5%92%8C%E4%BC%98%E5%8C%96/)  
[关于侧边栏社交链接的显示问题](https://github.com/iissnan/hexo-theme-next/issues/525)  
[Hexo Yelee主题侧边栏社交图标中的github图标不显示](https://www.codeleading.com/article/3849260970/)  
[hexo的next主题个性化配置](https://zhuanlan.zhihu.com/p/60424755)  

## 改变主题的布局样式

打开主题配置文件 `./themes/next/_config.yml` ，搜索 `scheme:` 关键字（大致在第 147--152 行），修改相应内容即可，如
```yaml
# Schemes
# scheme: Muse | Mist | Pisces | Gemini {choices}
scheme: Mist
#
# Muse：默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
# Mist：Muse 的紧凑版本，整洁有序的单栏外观
# Pisces：双栏 Scheme，小家碧玉似的清新
# Gemini：左侧网站信息及目录，块+片段结构布局
```

示例 **Examples**:
- Gemini / Pisces
- Mist / Muse

{% gp 4-3 %}
<img src="/images/2020-04/0412_hexonext_scheme_gemini.png">
<img src="/images/2020-04/0412_hexonext_scheme_pisces.png">
<img src="/images/2020-04/0412_hexonext_scheme_mist.png">
<img src="/images/2020-04/0412_hexonext_scheme_muse.png">
{% endgp %}
<!--Hello-->
<br>

*SEARCH*  
[侧边栏设置 | Hexo和NexT主题个性配置和优化](https://otuki.top/Hexo%E5%92%8CNexT%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E9%85%8D%E7%BD%AE%E5%92%8C%E4%BC%98%E5%8C%96/)  
next misc 布局  
[Hexo添加自定义分类菜单项并定制页面布局](https://finisky.github.io/2019/02/24/customizedcategory/)  
[修改hexo的主题nexT中的Pisces主题宽度](https://blog.csdn.net/csdnsr/article/details/78300820)  
[HEXO搭配Next主题修改博客](https://blog.codesfile.com/2017/12/16/HEXO%E6%90%AD%E9%85%8DNext%E4%B8%BB%E9%A2%98%E4%BF%AE%E6%94%B9%E5%8D%9A%E5%AE%A2/)  

## 评论系统

### 给整个博客添加评论系统
<!--为-->

ref: [使用来必力为博客添加评论系统](https://sherlockgy.github.io/2018/06/01/%E4%BD%BF%E7%94%A8%E6%9D%A5%E5%BF%85%E5%8A%9B%E4%B8%BA%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/) | [设置VsCode自动换行](https://sherlockgy.github.io/2018/09/01/%E8%AE%BE%E7%BD%AEVsCode%E8%87%AA%E5%8A%A8%E6%8D%A2%E8%A1%8C/)  

使用韩国产品 [来必力](https://livere.com/)，首先注册一个账号。  
*注意:* 我先用 Chrome 注册，这一步卡在了验证码，一直提示 "验证码不匹配"，无法继续操作；所以换到火狐尝试，仍然没能验证邮箱，先是登录提示密码不正确，然后试图找回密码时，莫名其妙地自己登入了，然后就继续后面流程了。  

注册成功后点击最上方的安装，即可获取 uid ，复制该 `uid` 代码。  
- 点击 "安装"，选择 City 版用于安装
  <img src="/images/2020-04/0412_LiveRe1.png" width="97%">

- 输入个人网站地址，即 `https://your-username/github.io`
  <img src="/images/2020-04/0412_LiveRe2.png" width="97%">
  
- 从 "一般网站" 代码中复制 `data-uid` 的值
  备注：最后面的两个 `==` 好像复制不复制都不影响，如果没有的话貌似加载会慢一点，不过差别也不是太大
  <img src="/images/2020-04/0412_LiveRe3p.png" width="97%">

然后打开主题配置文件 `./themes/next/_config.yml`，搜索 `livere_uid` ，将其前的 `#` 注释符号去掉，在后面填入方才复制的 uid 即可。


### 关掉某一页面的评论系统

**出现问题：** 到此为止，评论系统可以正常显示了，但是点击 Category / Tags 页面会发现它们的下方也会出现评论系统。那么怎样恢复正常呢？  ref: [个人博客网站接入来必力评论系统](https://blog.csdn.net/xiangzhihong8/article/details/77703791)  
找到主题相关配置文件 `./themes/next/layout/_partials/comments.swig`，修改该文件中条件，即在最后追加 LiveRe 是否引用的判断逻辑。**注意** next 中已包含此步。  
**备注**，原代码在 `./themes/next/layout/_partials/comments.swig` 的第 33--36 行，即
```yaml
  {% elseif theme.livere_uid %}
    <div class="comments" id="comments">
      <div id="lv-container" data-id="city" data-uid="{{ theme.livere_uid }}"></div>
    </div>
```

**Solution** refs:  
- NexT 主题配置 [hexo的Next创建tags](https://www.jianshu.com/p/03d3da9a1b68) , [如何关闭新建页面的评论功能？](https://theme-next.iissnan.com/faqs.html)  
- LiveRe 管理页面 [https://livere.com/insight/myCode](https://livere.com/insight/myCode)  

真正能解决此项问题的办法是：  
找到 `source/categories/index.md` 和 `source/tags/index.md` ，编辑其中的内容，即在结尾增加一行 `comments: false`，如下所示
```markdown
---
title: tags / categories
date: 2018-07-13 01:23:06 / 01:23:24

type: "tags" / "categories"
layout: "tags" / "categories"
comments: false
---
```

### Search Refs Record
**Search:**  
来必力 tags 页面也出现  
[Hexo搭建的GitHub博客之优化大全](https://zhuanlan.zhihu.com/p/33616481)  
[进阶(二)：hexo博客配置](https://champyin.com/2018/09/19/%E8%BF%9B%E9%98%B6-%E4%BA%8C-%EF%BC%9Ahexo%E5%8D%9A%E5%AE%A2%E9%85%8D%E7%BD%AE/)  
[Hexo-NexT配置超炫网页效果](https://www.jianshu.com/p/9f0e90cc32c2)  
next tags 取消评论  
[添加「标签」页面](https://theme-next.iissnan.com/theme-settings.html)  
[如何关闭新建页面的评论功能？](https://theme-next.iissnan.com/faqs.html)  
next tags页面 怎么生成  
[iissnan hexo-theme-next: 创建标签云页面](https://github.com/iissnan/hexo-theme-next/wiki/%E5%88%9B%E5%BB%BA%E6%A0%87%E7%AD%BE%E4%BA%91%E9%A1%B5%E9%9D%A2)  
[iissnan hexo-theme-next: 创建分类页面](https://github.com/iissnan/hexo-theme-next/wiki/%E5%88%9B%E5%BB%BA%E5%88%86%E7%B1%BB%E9%A1%B5%E9%9D%A2)  
[hexo的Next创建tags](https://www.jianshu.com/p/03d3da9a1b68)  
[Hexo使用攻略-添加分类及标签](https://linlif.github.io/2017/05/27/Hexo%E4%BD%BF%E7%94%A8%E6%94%BB%E7%95%A5-%E6%B7%BB%E5%8A%A0%E5%88%86%E7%B1%BB%E5%8F%8A%E6%A0%87%E7%AD%BE/)  

## 文章加密

hexo 博客加密  
[hexo文章加密](https://www.jianshu.com/p/44e211829447)  
[Hexo-blog-encrypt，给博客文章加密](https://xsin.gitee.io/2019/01/11/hexo-blog-encrypt/)  
[Hexo博客文章加密](https://www.jianshu.com/p/e4203ee066e5)  


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
说明: [] 里写链接文字，() 里写链接地址, () 中的 "" 中可以为链接指定 title 属性，title 属性可加可不加。title 属性的效果是鼠标悬停在链接上会出现指定的 title 文字。``[链接文字](链接地址 "链接标题")`` 这样的形式。链接地址与链接标题前有一个空格。

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
<img src="/images/?.png"> x n
{% endgp %}
```

| n | r-c | result |
|---|-----|--------|
| 2 | 1-2 | 2 |
| 3 | 1-3 or 1-2 | 3 |
| 4 | 4-3 or 5-3 | 2,2 |
| 4 | 6-5 or 8-7 or 5-4 | 3,1 |
| 4 | 1-4 or 1-5 | 3,? |
| 5 | 5-3 or 7-4 | 2,3 |
| 5 | 5-2 or 6-3 | 2,1,2 |
| 5 | 8-7 | 3,2 |
| 6 | 6-3 | 2,1,3 |
| 6 | 7-4 | 2,3,1 |
| 6 | 7-3 | 2,2,2 |
| 6 | 8-7 | 3,3 |
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

另外，若是有几张图不好排列的话，可以考虑用 ``<img src="">`` 来占位，如下是 ``两行三列 (其中位置 4 为空，起始点为 1)`` 和 ``三行两列 (图分组为 1-2-1 模式)`` 的代码：
```markdown
{% gp 8-7 %}
<img src="http://seaborn.pydata.org/_images/regression_17_0.png">
<img src="http://seaborn.pydata.org/_images/regression_19_0.png">
<img src="http://seaborn.pydata.org/_images/regression_21_0.png">
<img src="">
<img src="http://seaborn.pydata.org/_images/regression_23_0.png">
<img src="http://seaborn.pydata.org/_images/regression_25_0.png">
{% endgp %}

{% gp 7-3 %}
<img src="http://seaborn.pydata.org/_images/categorical_36_0.png">
<img src="">
<img src="http://seaborn.pydata.org/_images/categorical_38_0.png">
<img src="/images/2020-03/0327_sns_plot_category2_db2.png">
<img src="">
<img src="http://seaborn.pydata.org/_images/categorical_40_0.png">
{% endgp %}
```
<!--Hello World-->

附：如果 `hexo s` 后发现页面显示不正常，可以将 ``<!--"Hello World (optional)"-->`` 注释加在出现不正常的地方 (表现出不正常的位置 / 发现不正常前的最后修改部分)，一般情况下都可以恢复。


## Q & A

# Plugins 插件
<!--Updated: 2020.4.16 13:11-->

## 数学公式
ref: [hexo中插入数学公式](http://stevenshi.me/2017/06/26/hexo-insert-formula/)

> 原生hexo并不支持数学公式，需要安装插件 mathJax。[mathJax](https://www.mathjax.org/) 是一款运行于浏览器中的开源数学符号渲染引擎，使用 mathJax 可以方便的在浏览器中嵌入数学公式。mathJax 使用网络字体产生高质量的排版，因此可适应各种分辨率，它的显示是基于文本的而非图片，因此显示效果更好。这些公式可以被搜索引擎使用，因此公式里的符号一样可以被搜索引擎检索到。

### 安装
```shell
$ npm install hexo-math --save
```

i.e., 
```shell
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-math --save

> hexo-math@3.0.4 postinstall /home/ubuntu/eustomaqua.github.io/hexo-next/node_modules/hexo-math
> cd ../.. && npm install --save hexo-inject

^C[..................] / rollbackFailedOptional: verb npm-session 50e6c5afa624b8
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ npm install hexo-math --save

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
added 8 packages from 5 contributors, removed 3 packages and audited 3632 packages in 137.766s
found 203 vulnerabilities (136 low, 5 moderate, 62 high)
  run `npm audit fix` to fix them, or `npm audit` for details
+ hexo-math@3.0.4
updated 1 package and audited 3575 packages in 166.293s
found 195 vulnerabilities (136 low, 5 moderate, 54 high)
  run `npm audit fix` to fix them, or `npm audit` for details
ubuntu@ubuntu-VirtualBox:~/eustomaqua.github.io/hexo-next$ 
```

### 配置

- 在站点配置文件 `./_config.yml` 的末尾添加
```yaml
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    # src: custom_mathjax_source
    config:
      # MathJax config
```
- 在 NexT 主题配置文件 `./themes/next/_config.yml` 中将 mathJax 设为 true
```yaml
# MathJax Support
mathjax:
  enable: true
  per_page: true # false
  cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
```

- \* 也可以在文章的开始集成插件支持，但不建议这么做
```markdown
<script type="text/javascript"
   src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

**Backup:** default `./themes/next/_config.yml`
```yaml
# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------

# Math Equations Render Support
math:
  enable: false

  # Default(true) will load mathjax/katex script on demand
  # That is it only render those page who has 'mathjax: true' in Front Matter.
  # If you set it to false, it will load mathjax/katex srcipt EVERY PAGE.
  per_page: true

  engine: mathjax
  #engine: katex

  # hexo-rendering-pandoc (or hexo-renderer-kramed) needed to full MathJax support.
  mathjax:
    # Use 2.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/mathjax@2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For newMathJax CDN (cdnjs.cloudflare.com) with fallback to oldMathJax (cdn.mathjax.org).
    #cdn: //cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For direct link to MathJax.js with CloudFlare CDN (cdnjs.cloudflare.com).
    #cdn: //cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML
    # For automatic detect latest version link to MathJax.js and get from Bootcss.
    #cdn: //cdn.bootcss.com/mathjax/2.7.1/latest.js?config=TeX-AMS-MML_HTMLorMML

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin)
  # needed to full Katex support.
  katex:
    # Use 0.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/katex@0.7.1/dist/katex.min.css
    # CDNJS, provided by cloudflare, maybe the best CDN, but not works in China
    #cdn: //cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.css
    # Bootcss, works great in China, but not so well in other region
    #cdn: //cdn.bootcss.com/KaTeX/0.7.1/katex.min.css

# Han Support
# Dependencies: https://github.com/theme-next/theme-next-han
han: false
```

### 使用
公式 (Equation) 插入格式
```markdown
$数学公式$  行内 不独占一行
$$数学公式$$  行间 独占一行
```

### 示例

```markdown
---
title: MathJax Support
date: 2020-04-16 10:41:40
tags:
mathjax: true
---
```

### 语法格式

#### 上标与下标

使用 ^ 表示上标，使用 _ 表示下标，如果上下标的内容多于一个字符，可以使用大括号括起来：  
e.g., ``$$f(x) = a_1x^n + a_2x^{n-1} + a_3x^{n-2}$$``  
$$f(x) = a_1x^n + a_2x^{n-1} + a_3x^{n-2}$$

如果左右两边都有上下标可以使用 \sideset 语法：  
e.g., ``$$\sideset{^n_k}{^x_y}a$$``  
$$\sideset{^n_k}{^x_y}a$$

#### 括号

在 markdown 语法中，, $, {, }, _ 都是有特殊含义的，所以需要加 \ 转义。小括号与方括号可以使用原始的 () [] 大括号需要转义 \ 也可以使用 \lbrace 和 \rbrace  

e.g., 
```markdown
$$ \{x*y\} $$

$$ \lbrace x*y \rbrace $$
```
$$\{x*y\}$$

$$\lbrace x*y \rbrace$$

原始符号不会随着公式大小自动缩放，需要使用 \left 和 \right 来实现自动缩放：
e.g., ``$$\left \lbrace \sum_{i=0}^n i^3 = \frac{(n^2+n)(n+6)}{9} \right \rbrace$$``
$$\left \lbrace \sum_{i=0}^n i^3 = \frac{(n^2+n)(n+6)}{9} \right \rbrace$$

不使用 \left 和 \right 的效果：
i.e., ``$$ \lbrace \sum_{i=0}^n i^3 = \frac{(n^2+n)(n+6)}{9}  \rbrace$$``
$$ \lbrace \sum_{i=0}^n i^3 = \frac{(n^2+n)(n+6)}{9}  \rbrace$$

#### 分数与开方

可以使用 \frac 或者 \over 实现分数的显示：
```markdown
$\frac xy$
$ x+3 \over y+5 $
```
分别显示为 $\frac xy$ 和 $ x+3 \over y+5 $

开方使用\sqrt:  
```markdown
$ \sqrt{x^5} $
$ \sqrt[3]{\frac xy} $
```
分别显示为 $\sqrt{x^5}$ 和 $\sqrt [3]{\frac xy}$

**Notice:** $\sqrt [3]{\frac{x}{y}}$  
***遗留问题***： 开根号不能正常显示，尚未找到解决方法。

$\sqrt [3]{2}$

#### 求和与积分

求和使用 \sum ，可加上下标；积分使用 \int ，可加上下限；双重积分用 \iint ：
```markdown
$ \sum_{i=0}^n $
$ \int_1^\infty $
$ \iint_1^\infty $
```
分别显示为 $ \sum_{i=0}^n $ 、 $ \int_1^\infty $ 以及 $ \iint_1^\infty $

#### 极限
极限使用 \lim ：
e.g., ``$ \lim_{x \to 0} $`` 
显示为 $ \lim_{x \to 0} $

#### 表格与矩阵

表格样式 lcr 表示居中，| 加入一条竖线，\hline 表示行间横线，列之间用 & 分隔，行之间用 \ 分隔  
```markdown
$$\begin{array}{c|lcr}
n & \text{Left} & \text{Center} & \text{Right} \\\\
\hline
1 & 1.97 & 5 & 12 \\\\
2 & -11 & 19 & -80 \\\\
3 & 70 & 209 & 1+i \\\\
\end{array}$$
```
显示效果为  
$$\begin{array}{c|lcr}
n & \text{Left} & \text{Center} & \text{Right} \\\\
\hline
1 & 1.97 & 5 & 12 \\\\
2 & -11 & 19 & -80 \\\\
3 & 70 & 209 & 1+i \\\\
\end{array}$$

表格的插入也可以使用以下方式： 
```markdown
|名称|说明|
|---|---|---|
|temperature|  室内温度 |
|set temperature|  设定温度 |
|height|  室内高度 |
```
显示效果为  

|名称|说明|
|---|---|---|
|temperature|  室内温度 |
|set temperature|  设定温度 |
|height|  室内高度 |

矩阵显示和表格很相似  
```markdown
$$\left[
\begin{matrix}
V_A \\\\
V_B \\\\
V_C \\\\
\end{matrix}
\right] =
\left[
\begin{matrix}
1 & 0 & L \\\\
-cosψ & sinψ & L \\\\
-cosψ & -sinψ & L
\end{matrix}
\right]
\left[
\begin{matrix}
V_x \\\\
V_y \\\\
W \\\\
\end{matrix}
\right] $$
```
展示为  
$$\left[
\begin{matrix}
V_A \\\\
V_B \\\\
V_C \\\\
\end{matrix}
\right] =
\left[
\begin{matrix}
1 & 0 & L \\\\
-cosψ & sinψ & L \\\\
-cosψ & -sinψ & L
\end{matrix}
\right]
\left[
\begin{matrix}
V_x \\\\
V_y \\\\
W \\\\
\end{matrix}
\right] $$

还有其他矩阵如内联矩阵增广矩阵方程组等，此处未补充。

### Refs

github pages 英文公式  
[怎样用 Github Pages 建立博客（2. 进阶）](https://wklchris.github.io/Advanced-blog-skills.html)  
[使用Jekyll在GitHub上搭建个人博客](https://lyk6756.github.io/jekyll/2017/02/26/build_blog.html)  
[github上利用jekyll搭建自己的blog的操作顺序？](https://www.zhihu.com/question/30018945)  
[用 jekyll + Github Pages搭建个人博客](https://blog.csdn.net/u013553529/article/details/54588010)  
hexo 数学公式  
[hexo中插入数学公式](http://stevenshi.me/2017/06/26/hexo-insert-formula/)  
[在Hexo中渲染MathJax数学公式](https://www.jianshu.com/p/7ab21c7f0674)  
[Hexo 的 Next 主题中渲染 MathJax 数学公式](https://blog.csdn.net/wgshun616/article/details/81019687)  
[在 Hexo 中使用 MathJax 渲染数学公式](https://abelsu7.top/2018/10/29/hexo-mathjax/)  

hexo 公式开方  
[markdown之数学公式语法](http://xwxz.github.io/tools-markdown/)  
[在Hexo中使用MathJax插入数学公式](http://blog.mobing.net/content/hexo/hexo-mathjax.html)  
latex 数学公式  
[常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)  

hexo 个别公式不加载  
[Hexo Math Support | 冯玮的博客](https://fwzju.com/2018/06/24/math-support/)  
[Hexo+Github: 个人博客网站搭建完全教程(看这篇就够了)-上半部分](https://zhuanlan.zhihu.com/p/80140564)  
[Hexo博客(13)添加MathJax数学公式渲染](http://masikkk.com/article/hexo-13-MathJax/)  
[在Hexo中渲染MathJax数学公式](http://wangxin123.com/2017/09/20/%E5%9C%A8Hexo%E4%B8%AD%E6%B8%B2%E6%9F%93MathJax%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F/)  

hexo sqrt 有问题  
[Latex 的渲染问题](https://github.com/hexojs/hexo/issues/2115)  
[关于 hexo 对文章渲染解析 的问题](https://www.v2ex.com/t/510207)  
[结合MathType和MathJax在Hexo博客中插入数学公式](https://zhuanlan.zhihu.com/p/108766968)  
[hexo 迷之代码高亮？](https://www.zhihu.com/question/37222515)  
[Hexo 中使用数学公式](https://suzhouxing.github.io/techive/2017/09/03/HexoMathSupport/)  


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
~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
~/eustomaqua.github.io$ date -s
date：选项需要一个参数 -- s
Try 'date --help' for more information.
~/eustomaqua.github.io$ date --s
date：选项 ‘--set’ 需要一个参数
Try 'date --help' for more information.
~/eustomaqua.github.io$ date --help
用法：date [选项]... [+格式]
　或：date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
Display the current time in the given FORMAT, or set the system date.
~/eustomaqua.github.io$ date
Thu Mar 26 18:09:05 CDT 2020



~/eustomaqua.github.io$ sudo apt-get install apt-transport-https ca-certificates -y
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
~/eustomaqua.github.io$ sudo update-ca-certificates
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
~/eustomaqua.github.io$ 
~/eustomaqua.github.io$ 



~/eustomaqua.github.io$ date
Thu Mar 26 18:12:27 CDT 2020
~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
~/eustomaqua.github.io$ openssl s_client -showcerts -servername git.mycompany.com -connect git.mycompany.com:443 </dev/null 2>/dev/null | sed -n -e '/BEGIN\ CERTIFICATE/,/END\ CERTIFICATE/ p'  > git-mycompany-com.pem
~/eustomaqua.github.io$ 
~/eustomaqua.github.io$ date
Thu Mar 26 18:14:32 CDT 2020
~/eustomaqua.github.io$ 



~/eustomaqua.github.io$ git push
fatal: unable to access 'https://github.com/eustomaqua/eustomaqua.github.io.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
~/eustomaqua.github.io$ git config
用法：git config [<选项>]
~/eustomaqua.github.io$ git config http.sslverify
~/eustomaqua.github.io$ git config http.sslverify --get
~/eustomaqua.github.io$ git config http.sslverify false
~/eustomaqua.github.io$ 
```

### RPC failed; curl 56 GnuTLS recv error (-54)
RPC failed; curl 56 GnuTLS recv error (-54): Error in the pull function.

```bash
~/eustomaqua.github.io$ git push
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
~/eustomaqua.github.io$ 


~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

    git-mycompany-com.pem

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
~/eustomaqua.github.io$ whereis git-mycompany-com.pem
git-mycompany-com:
~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
~/eustomaqua.github.io$ 



~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
~/eustomaqua.github.io$ git push
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
~/eustomaqua.github.io$ git status
位于分支 hexo-next
您的分支领先 'origin/hexo-next' 共 3 个提交。
  （使用 "git push" 来发布您的本地提交）
无文件要提交，干净的工作区
~/eustomaqua.github.io$ 
```

## FAQ

# \*References

**Helpful:**  
[Markdown 语法整理](https://guo365.github.io/study/Markdown.html#11)  
[Markdown 书写风格指南](https://einverne.github.io/markdown-style-guide/zh.html)  

