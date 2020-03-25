---
title: Hexo+NexT, Trouble Solver
date: 
updated: 2020-03-25 21:36:22
categories:
  - Records
tags:
  - Hexo
  - Debug
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


## Questions?


# NexT Theme (主题)
## Questions? (with Error log)

# \*References

