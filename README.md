# 简介

这是一个因为目前大部分漫画站都不支持双页显示所以经常遇到漫画出现跨页大图被分割成两页的人为了能看到跨页大图而写的油猴脚本。为漫画站增加了双页阅读模式并优化了使用体验，支持站点和各个站点的功能增强见目录。针对支持站点以外的网站，也可以使用简易阅读模式来双页阅读漫画。

# 目录

- [安装](#安装)
- [漫画阅读模式](#漫画阅读模式)
- [脚本设置](#脚本设置)
- [支持站点](#支持站点)
  - [百合会](#百合会)
    - [记录阅读历史](#记录阅读历史)
    - [体验优化](#体验优化)
  - [百合会新站](#百合会新站)
  - [动漫之家](#动漫之家)
    - [看被封漫画](#看被封漫画)
    - [导出导入漫画订阅/历史记录](#导出导入漫画订阅/历史记录)
    - [优化网页右上角用户信息栏的加载](#优化网页右上角用户信息栏的加载)
    - [解除吐槽的字数限制](#解除吐槽的字数限制)
  - [ehentai](#ehentai)
    - [nhentai匹配](#nhentai匹配)
      - [漫画](#漫画)
      - [Tag](#Tag)
  - [nhentai](#nhentai)
    - [彻底屏蔽漫画](#彻底屏蔽漫画)
    - [自动翻页](#自动翻页)
- [简易漫画阅读模式](#简易漫画阅读模式)

# 最近更新

## 2019.7.17

### 修改

- 现在更新后只会提示一次版本更新

### 新增

- 卷轴模式。可在侧边栏切换。
- dm5、manhuagui、manhuadb 的适配

### 修复

- 下载文件未在文件名前补零的 bug

## 2019.6.12

### 修复

- 在 ehentai 加载 nhentai 漫画后无法正常进入阅读模式的错误

## 2019.5.23

### 修复

- 无法在百合会正常运作的 Bug

[完整更新日志](https://github.com/hymbz/ComicReadScript/blob/master/UpdateLog.md)

# 前置需求

使用脚本需要安装有 Tampermonkey ，直接到 [官网](http://tampermonkey.net/index.php) 根据自己的浏览器和浏览器版本下载对应扩展安装即可。

# 安装

[greasyfork](https://greasyfork.org/zh-CN/scripts/374903-comicread)

# 漫画阅读模式

漫画双页模式下默认从右到左阅读。

## 脚本设置

通过点击浏览器扩展栏里的油猴按钮，在弹出菜单中点击「漫画阅读设置」打开当前网站的相关设置。点击功能标题可以禁用功能。

## 侧边栏

### 显示

PC上，将鼠标移动至左侧边缘显示。

平板上，右滑显示，左滑关闭。

### 功能介绍

由上至下分别是：

- ![](http://wx2.sinaimg.cn/large/6d4090c8gy1fu851h097zj200o00o04h.jpg)双页模式：点击切换双页单页显示。
- ![](http://wx3.sinaimg.cn/large/6d4090c8gy1fu853ttim9j200o00o03p.jpg)页面填充：用于使当前图片流的顺序符合正常漫画的顺序，详见[页面填充](#页面填充)
- ![](http://ws3.sinaimg.cn/large/6d4090c8gy1fu858xbdvyj200o00o06y.jpg)点击翻页：可通过点击屏幕来翻页。（翻页可以通过鼠标滚轮、方向键、空格翻页，但因为是滚动一次翻一页，所以在平板或笔记本上不用鼠标很难精确地只翻一页，于是就有了这个功能，另外也能通过上下滑动来翻页）
- ![](http://wx4.sinaimg.cn/large/6d4090c8gy1fu85e8gcg0j200o00o04a.jpg)阅读进度：在右侧用一列小圆点显示总页数和当前页，点击对应圆点可以直接跳转至目标页数。
- ![](http://wx4.sinaimg.cn/large/6d4090c8gy1fu85gvp8fvj200o00o070.jpg)夜间模式：顾名思义。
- ![](http://ws3.sinaimg.cn/large/6d4090c8gy1fu85itqh26j200o00o06x.jpg)放大：顾名思义。（除点击按钮外，也可通过双击任意位置打开，开启点击翻页时除外，防止误点击。）
- ![](http://wx1.sinaimg.cn/large/6d4090c8gy1fu85l7bbw0j200o00o06j.jpg)下载：顾名思义。
- ![](http://ws3.sinaimg.cn/large/6d4090c8gy1fu85mb5676j200o00o04k.jpg)退出：顾名思义。（通过侧边栏退出视作中途离开，下次进入阅读模式会从上次中途离开的地方看起。在结尾会有另一个退出的按钮「End」，通过 End 退出视作阅读结束，退出的同时会跳转至评论——如果有评论的话，下次进入阅读模式会从头开始）

## 页面填充

日漫一般奇数页在左，偶数页在右，所以为了保证被分割成两页后的跨页图能拼在一起，就得在第1页填充进一个空白页填补右页的空白。但因为平台和汉化组的原因，图片流中有可能出现跨页的大图，如果是不符合漫画页数顺序——左奇右偶——的大图（比如汉化组/平台/漫画的宣传图），为了之后的图片顺序能正确，就必须在其之后再添加填充页。

如果图片流中没有出现跨页大图，那「页面填充」的影响范围就是整个图片流；如果出现了一张跨页大图，已跨页大图为分割点，「页面填充」的影响范围将被分为两个。以此类推，图片流中出现的跨页大图将整个图片流分割为多块独立的流。通过侧边栏的页面填充按钮可以查看和修改当前流的「页面填充」的状态。

页面填充的开启与否需要视具体情况而定。一般来说，如果页数没被处理掉的话，直接将漫画页数调整到左奇右偶即可，不过一般漫画的页数都被汉化组处理掉了。没有页数的情况下，如果漫画图源够好，并且汉化组没有进行白边剪裁的话，在漫画顺序正确的情况下中间会有比较大的白边——即书的中缝，可以根据这一点来进行调整。如果汉化组进行了白边剪裁的话，就只能凭经验判断了:)

## 注意

一些站点使用了图片懒加载功能，图片只会在滚动至能被（或即将被）用户看见的位置后才会开始加载。此功能开启后，图片懒加载将会失效。

# 支持站点

## 百合会

### 入口

漫画阅读模式的入口在帖子一楼顶端![](http://wx3.sinaimg.cn/large/6d4090c8gy1frkne5skvqj20my02gmx4.jpg)

将鼠标移动到这个位置后，就可以看到新增的「漫画阅读」按钮![](http://wx3.sinaimg.cn/large/6d4090c8gy1frknejh46wj20my02ajrd.jpg)

> 脚本默认自动进入漫画阅读模式，可在设置中关闭

### 记录阅读历史

这个功能是用来快速回到帖子上次阅读进度的。开启后，每个帖子后面都会跟着一个跳转至上次阅读位置的TAG，点击即可跳转至上次阅读进度（阅读进度不仅包括了页数也包括了楼层数），后面跟着的数字是上次阅读后新增的回复数。

![](http://wx3.sinaimg.cn/large/6d4090c8gy1frkpi4a2ikj207u00yq2q.jpg)

颜色默认是论坛的深褐色，可以在设置中改成任意喜欢的颜色。

阅读进度默认永久保存，可在设置中设置保留天数。如果一个已经记录了进度的帖子在超过保留天数后依然没有点进去阅读的话其阅读进度就会被删除。想删掉所有阅读进度的话就设为0，保存设置，刷新，即可。-1表示永久保存。

### 体验优化

这是些无关紧要的小功能的集合。

#### 关闭快捷导航的跳转

顶部导航条的快捷导航可以方便地在各个板块之间跳转，但默认情况下只能通过鼠标悬浮的方式显示其板块菜单，直接点击的话会跳转至论坛主页，这在平板上很不方便，所以有了这个功能。功能很简单，就是关掉快捷导航的点击跳转，只保留悬浮显示菜单的功能。

#### 固定导航条

快捷导航的跳转是很方便，但每次跳转都要把网页滚到顶部去就有点麻烦了。开启这个功能可以将顶部的导航条固定住，不管怎么滚动都始终保持在页面顶部。

#### 修正点击页数时的跳转判定

![](http://wx3.sinaimg.cn/large/6d4090c8gy1frkqbxkztij20vb01c0sn.jpg)

明明在板块顶部有个“新窗”的选项来选择帖子的默认打开位置，但即使勾上了新窗，通过点击帖子后面的页数打开的页面还是会在当前页打开。开启这个功能可以补上这个缺漏。

## 百合会新站

### 入口

在漫画页标题下的功能区。

因为百合会新站只能翻页看，所以如果要用阅读模式看的话需要加载其他页面的图片。未加载时按钮是禁用状态，点击开始加载，加载完成后按钮将会恢复。

### 顶栏菜单在鼠标移上时显示

## 动漫之家

### 入口

在漫画页顶部右上角。

> 脚本默认自动进入漫画阅读模式，可在设置中关闭

### 看被封漫画

被封漫画有两种情况，一种依然保留着漫画详情页，只是目录被封了而已，对此脚本将恢复目录，之后像平常那样观看即可；另一种则连详情页都删了，对此请通过 [https://dmzj.nsapps.cn/](https://dmzj.nsapps.cn/) 搜索进入漫画的详情页，脚本会生成一个简单的目录页，点击目录的对应话数后会跳转到另一个页面加载漫画，加载需要一定时间，视网速而定。加载好后直接进入阅读模式，退出阅读模式后可以再通过油猴菜单里的「进入阅读模式」进入阅读模式。

开启此功能后，原先的「因版权、国家法规...」的提示将被倒转，方便判断是否开启此功能，等获取到了漫画信息后提示就会被替换成漫画目录了。

### 导出导入漫画订阅/历史记录

在「[我的订阅](https://i.dmzj.com/subscribe)」和「[浏览历史](https://i.dmzj.com/record)」页面添加了导出导入功能按钮。

点击导出按钮可将记录以 Json 格式导出，导出数据为名字（name）、网页端网址（url）、漫画 id（id）。

点击导入按钮后选择本地 Json 文件，可按 Json 文件中记录的漫画数据导入，将根据导入的数据自动订阅未订阅漫画。导入时按钮上的计数器将显示剩余订阅漫画数量。导入时其实只需要漫画 id（id）这一项数据，另外两项数据仅为备份，以防万一。

### 优化网页右上角用户信息栏的加载

因为动漫之家服务器的问题，右上角的用户信息栏有时候无法自己加载出来，开启此功能后可以帮它一把。

### 解除吐槽的字数限制

### 其他

去掉了一些广告和无用的元素。漫画页直接用 stylish 上 pgain2004 的「[动漫之家暗色调漫画阅读页 (布局精简)](https://userstyles.org/styles/119945/theme)」进行了美化，在此表示感谢。不喜欢暗色调的话也可以调成白色的，漫画页的色调和阅读模式中夜间模式的开启与否相关联。

## ehentai

### 入口

![](https://greasyfork.org/system/screenshots/screenshots/000/013/160/original/Snipaste_2018-11-28_17-12-03.png)

在漫画详情页右侧边栏。开启功能后会多出一个「Load comic」按钮，点击后开始加载漫画，加载完毕后按钮变为「Read」，点击开始阅读。加载过程中可以点击按钮，不等待全部图片加载完毕就直接进入阅读模式。但当加载图片过多时可能没法立刻进入阅读模式，需要等待脚本至少将图片加载请求发送完毕，另外因为图片加载可能不是顺序加载，所以也有可能出现缺页情况。

> 一些带有广告屏蔽功能的插件可能会影响 ehentai 上图片的显示，比如 Ghostery。

### nhentai匹配

#### 漫画

![](https://greasyfork.org/system/screenshots/screenshots/000/013/161/original/Snipaste_2018-11-28_17-15-42.png)

根据漫画标题匹配 nhentai 的本子，结果会以标签的形式显示在标签栏中，标签内容为 nhentai 上的漫画 ID ，鼠标悬停在标签上可以看到漫画标题。点击标签后，标签菜单有两个选项：「Jump to nhentai」—— 跳转至对应的 nhentai 网页、「Load comic」—— 直接在当前页加载 nhentai 的资源，加载完后可以直接用阅读模式阅读。相比 ehentai，nhentai 的资源加载更快，而且不会消耗配额。

#### Tag

![](https://greasyfork.org/system/screenshots/screenshots/000/013/162/original/Snipaste_2018-11-28_17-17-16.png)

将点击标签后显示的标签菜单里「Add New Tag」的按钮改为「Search nhentai」，点击跳转至 nhentai 相同标签的结果页。方便搜索那些在 ehentai 上被删的资源。

## nhentai

### 入口

在漫画详情页收藏按钮的旁边。开启功能后会多出一个「Load comic」按钮，点击后开始加载漫画，加载完毕后按钮变为「Read」，点击开始阅读。加载过程中可以点击按钮，不等待全部图片加载完毕就直接进入阅读模式。但当加载图片过多时可能没法立刻进入阅读模式，需要等待脚本至少将图片加载请求发送完毕，另外因为图片加载可能不是顺序加载，所以也有可能出现缺页情况。

### 彻底屏蔽漫画

nhentai 的屏蔽机制是在被屏蔽漫画封面加上一层半透明遮罩，所以对于那些屏蔽范围比较大的人来说，在首页或搜索结果里连续翻上几页都是满屏的被屏蔽漫画完全是家常便饭。开启此功能后，被屏蔽漫画将被彻底屏蔽，不会再出现在首页或搜索结果里了。

### 自动翻页

接上，如果屏蔽范围比较大，有时可能需要翻上好几页才能找到想看的漫画，所以有了该功能，当网页滚动至底部时将自动在底部加载下一页的内容。如果开启了「彻底屏蔽漫画」功能，将自动跳过没有结果的页面。加载时底部会有加载条表示正在加载，当加载条停止时表示已到最后页。

## 简易漫画阅读模式

用于在支持站点以外的网站双页阅读漫画。开启后，将把当前网页中显示的所有宽高均大于 500 像素的图片作为图源加载。

有些网站使用了懒加载，需要先提前触发，确保图片加载完毕。网页启用了懒加载，但部分图片未加载的话脚本会提示。

### 入口

点击浏览器扩展栏里的油猴按钮，在弹出菜单中点击「进入简易漫画阅读模式」。
