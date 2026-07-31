# Welcome to MkDocs

<!--
For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
-->


```shell
source activate py3e

mkdocs new docs
cd docs
mkdocs build
mkdocs serve

sphinx-quickstart
> Separate source and build directories (y/n) [n]: y
> Project name: eustomaqua
> Author name(s): eustomaqua
> Project release []: 0.1
> Project language [en]: en
make html
```

[河图](https://hetu-music.com/zh-CN/song/351) Finale

**References**  
[Markdown](https://markdown.com.cn/basic-syntax/images.html)  
[自定义字体](https://blog.csdn.net/m0_63203517/article/details/131946304), [extra_css教程](https://wcowin.work/blog/Mkdocs/mkdocs2/#extra_javascript-%E5%92%8Cextra_css)  
[配置字体](https://mkdoc-material.llango.com/setup/changing-the-fonts/), [汉语字体](https://blog.wulited.com/tech/chnfonts/)  
<!--
![cover](https://hetu-music.com/_next/image?url=https%3A%2F%2Fcover.hetu-music.com%2Fcover%2Fproto.jpg&w=1200&q=75){width=50%}
-->
