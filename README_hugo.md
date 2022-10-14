# Personal Blog

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
$ hugo
$ hugo server
```

## refs
