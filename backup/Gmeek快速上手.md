> [!TIP]
[来源:Meekdai](https://blog.meekdai.com/post/Gmeek-kuai-su-shang-shou.html)

> [!NOTE]
[Gmeek](https://github.com/Meekdai/Gmeek) 一个博客框架，超轻量级个人博客模板，完全基于Github Pages 、 Github Issues 和 Github Actions，可以称作All in Github。不需要本地部署，从搭建到写作，只需要18秒，2步搭建好博客，第3步就是写作。

### 一、安装

> [!IMPORTANT]
安装及其简单，但是也要认真看下面的步骤，一步一步来。

1. 【创建仓库】点击通过模板创建仓库，建议仓库名称为XXX.github.io，其中XXX为你的github用户名。
2. 【启用Pages】在仓库的设置Settings中Pages->Build and deployment->Source下面选择Github Actions。
3. 【开始写作】打开一篇issue，开始写作，并且必须添加一个标签Label（至少添加一个），再保存issue后会自动创建博客内容，片刻后可通过https://XXX.github.io 访问（可进入Actions页面查看构建进度）。
4. 【手动全局生成】这个步骤只有在修改config.json 文件或者出现奇怪问题的时候，需要执行。
5. 通过Actions->build Gmeek->Run workflow->里面的按钮全局重新生成一次

> [!NOTE]
网友制作的视频教程：https://www.bilibili.com/video/BV1GM4m1m7ZD/

### 二、配置文件

> [!TIP]
按照安装步骤成功搭建好后，就可以阅读下面的内容修改配置文件啦。
注意修改配置文件后一定要手动全局生成一次，不然会报错。
如果对json格式不熟悉，建议先简单学习一下。

config.json 文件就是配置文件，在创建的仓库内可以找到，对应修改为自己的即可。

```
{
    "title":"Meekdai",
    "subTitle":"童话是一种生活态度，仅此而已。",
    "avatarUrl":"https://github.githubassets.com/favicons/favicon.svg",
    "GMEEK_VERSION":"last"
}
```
以上是必须的字段，下面是可以自定义字段的描述，可以选择加入到config.json中。

```
"displayTitle":"Meekdai",
"homeUrl":"http://blog.meekdai.com",
"faviconUrl":"https://github.githubassets.com/favicons/favicon.svg",
"email":"meekdai@163.com",
"startSite":"02/16/2015",
"filingNum":"浙ICP备20023628号",
"onePageListNum":15,
"singlePage":["about"],
"iconList":{"music":"M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8Zm8-6.5a6.5 6.5 0 1 0 0 13 6.5 6.5 0 0 0 0-13Z"},
"exlink":{"music":"https://music.meekdai.com"},
"commentLabelColor":"#006b75",
"yearColorList":["#bc4c00", "#0969da", "#1f883d", "#A333D0"],
"i18n":"CN",
"UTC":8,
"themeMode":"manual",
"dayTheme":"light",
"nightTheme":"dark_colorblind",
"urlMode":"pinyin",
"style":"",
"script":"",
"head":"",
"allHead":"",
"indexStyle":"",
"indexScript":"",
"showPostSource":1,
"rssSplit":"sentence",
"bottomText":"转载请注明出处",
"ogImage":"https://cdn.jsdelivr.net/gh/Meekdai/meekdai.github.io/logo64.jpg",
"primerCSS":"<link href='https://mirrors.sustech.edu.cn/cdnjs/ajax/libs/Primer/21.0.7/primer.css' rel='stylesheet' />",
"needComment":0,
```

> [!CAUTION]
最后一行配置末尾不需要逗号，其他行末尾都需要逗号（英文逗号）

配置参数    说明
title    【必填】博客标题
subTitle    【必填】博客描述&自述
avatarUrl    【必填】博客头像
GMEEK_VERSION    【必填】Gmeek版本，一般写last也可以用具体tag版本
displayTitle    用于头像后面的标题展示，如果和title一致则不用添加
homeUrl    博客的主页地址，自定义域名时需要配置
faviconUrl    页面的favicon地址，如果和avatarUrl一致则不用添加
email    用于自动提交仓库时用，不添加也可以
startSite    用于页面底部显示网站运行天数
filingNum    用于页面底部显示备案信息
onePageListNum    用于首页每页展示的文章数量
singlePage    自定义独立页面，例如about或者link等
iconList    用于定义singlePage按钮展示的SVG图标 (16px)，about和link内置无需定义
exlink    用于自定义首页右上角圆形按钮到外部链接功能，按钮图标定义在iconList中
commentLabelColor    用于自定义显示评论数量标签的颜色
yearColorList    用于自定义显示不同年份标签的颜色
i18n    用于定义博客语言，目前支持EN/CN/RU
UTC    用于定义时区
themeMode    用于定义主题模式，默认为manual，也可选择fix详细说明
dayTheme    用于定义亮主题
nightTheme    用于定义暗主题
urlMode    用于定义文章链接生成模式，目前支持pinyin/issue/ru_translit
style    用于自定义文章页CSS
script    用于自定义文章页JavaScript
head    用于自定义文章页head内容
allHead    用于自定义所有页面head内容
indexStyle    用于自定义首页CSS
indexScript    用于自定义首页JavaScript
showPostSource    设置为1则在文章页显示issue链接按钮，设置为0则不显示
rssSplit    设置RSS输出的截断符号，默认sentence为第一句话，可配置其他特殊符号
bottomText    用于设置文章页面右下角显示的内容
ogImage    用于设置Open Graph协议展示的图片
primerCSS    用于设置primer.css的CDN地址，默认使用南科大
needComment    用于设置是否需要评论功能，1开启评论，0关闭

### 三、常见问题

#### 1. 搭建不成功

多半是没有按照安装步骤来，其实搭建就这2步，不要自己乱点乱设置，就不会有问题。

案例一：Meekdai/Gmeek#14
案例二：Meekdai/Gmeek#18
案例二：Meekdai/Gmeek#20
#### 2. Actions执行失败

修改了config.json配置文件后，需要全局生成。另外label标签没有打会出现这个问题。
建议通过Actions->build Gmeek->Run workflow->里面的按钮全局重新生成一次

案例一：Meekdai/Gmeek#1
案例二：Meekdai/Gmeek#10
#### 3. 导入以前的文章

如需修改发布时间，可以在文章最后一行添加如下代码。里面的时间是采用时间戳的形式，可以用如下网站转换。

`<!-- ##{"timestamp":1490764800}## -->`
#### 4. 自定义单篇文章参数

自定义单篇文章页面的style和script

```
<!-- ##{"style":"<style>#postBody{font-size:20px}</style>"}## -->
<!-- ##{"script":"<script async src='//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js'></script>"}## -->
```
#### 5. 多种自定义参数

可同时一起添加多种自定义参数：

`<!-- ##{"script":"<script async src='//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js'></script>","style":"<style>#postBody{font-size:20px}</style>","timestamp":1490764800}## -->`
#### 6. 自定义全局文章参数

添加全局文章页面的style和script，在config.json文件中添加

```
"style":"<style>#postBody{font-size:20px}</style>",
"script":"<script async src='//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js'></script>",
```
#### 7. 置顶博客文章

只需要Pin issue后，手动全局生成一次即可。

#### 8. utteranc报错

如果在评论里面登录后评论报错，可直接按照提示安装utteranc app即可

Error: utterances is not installed on xxx/xxx.github.io. If you own this repo, install the app. Read more about this change in the PR.
#### 9. 删除文章

只需要Close issue或者Delete issue后，再手动全局生成一次即可。

### 四、进阶教程

Gmeek的可定制化功能非常高，下面的链接是一些更加高级的设置教程，还有插件的使用等。
https://meekdai.github.io/tag.html#Gmeek