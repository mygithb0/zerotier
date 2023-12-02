make: command not found 解决办法
白夜鬼魅
于 2021-06-30 15:31:54 发布
阅读量3.6w
收藏 29
点赞数 12
分类专栏： 日常问题及解决 文章标签： vim linux bash
版权
日常问题及解决 专栏收录该内容
77 篇文章 10 订阅
订阅专栏

出现错误：-bash: make: command not found
原因分析：一般出现这个-bash: make: command not found提示，是因为安装系统的时候使用的是最小化mini安装，系统没有安装make、vim等常用命令，直接sudo apt-get install安装下即可。
解决方法：

```
sudo apt-get update
sudo apt-get install  gcc automake autoconf libtool make
```



