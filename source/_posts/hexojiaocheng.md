---
title: hexojiaocheng
date: 2022-04-04 20:16:41
tags:
---

# Hexo简介
Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。大家可以进入hexo官网进行详细查看，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。

教程分三个部分，

第一部分：hexo的初级搭建还有部署到github page上，以及个人域名的绑定。
第二部分：hexo的基本配置，更换主题，实现多终端工作，以及在coding page部署实现国内外分流
第三部分：hexo添加各种功能，包括搜索的SEO，阅读量统计，访问量统计和评论系统等。
# 第一部分
hexo的初级搭建还有部署到github page上，以及个人域名的绑定。
# Hexo搭建步骤
1. 安装Git

windows：到git官网上下载,Download git,下载后会有一个Git Bash的命令行工具，以后就用这个工具来使用git。

linux：对linux来说实在是太简单了，因为最早的git就是在linux上编写的，只需要一行代码

sudo apt-get install git

2. 安装nodejs
Hexo是基于nodeJS编写的，所以需要安装一下nodeJs和里面的npm工具。

windows：nodejs选择LTS版本就行了。

linux：

sudo apt-get install nodejs
sudo apt-get install npm
安装完后，打开命令行

node -v
npm -v
检查一下有没有安装成功

顺便说一下，windows在git安装完后，就可以直接使用git bash来敲命令行了，不用自带的cmd，cmd有点难用。

3. 安装hexo
前面git和nodejs安装好后，就可以安装hexo了，你可以先创建一个文件夹blog，然后cd到这个文件夹下（或者在这个文件夹下直接右键git bash打开）。

输入命令

npm install -g hexo-cli
依旧用hexo -v查看一下版本

至此就全部安装完了。

接下来初始化一下hexo

hexo init myblog
这个myblog可以自己取什么名字都行，然后

cd myblog //进入这个myblog文件夹
npm install
新建完成后，指定文件夹目录下有：

node_modules: 依赖包
public：存放生成的页面
scaffolds：生成文章的一些模板
source：用来存放你的文章
themes：主题
** _config.yml: 博客的配置文件**
hexo g
hexo server
打开hexo的服务，在浏览器输入localhost:4000就可以看到你生成的博客了。

4. GitHub创建个人仓库

创建一个和你用户名相同的仓库，后面加.http://github.io，只有这样，将来要部署到GitHub page的时候，才会被识别，也就是http://xxxx.github.io，其中xxx就是你注册GitHub的用户名。

5. 生成SSH添加到GitHub
回到你的git bash中，

git config --global user.name "yourname"
git config --global user.email "youremail"
这里的yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱。这样GitHub才能知道你是不是对应它的账户。

可以用以下两条，检查一下你有没有输对

git config user.name
git config user.email
然后创建SSH,一路回车

ssh-keygen -t rsa -C "youremail"
这个时候它会告诉你已经生成了.ssh的文件夹。在你的电脑中找到这个文件夹。

6. 将hexo部署到GitHub
这一步，我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 _config.yml，翻到最后，修改为 YourgithubName就是你的GitHub账户

deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
这个时候需要先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。

npm install hexo-deployer-git --save
然后

hexo clean
hexo generate
hexo deploy
其中 hexo clean清除了你之前生成的东西，也可以不加。 hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写 hexo deploy 部署文章，可以用hexo d缩写

注意deploy时可能要你输入username和password。

得到下图就说明部署成功了，过一会儿就可以在http://yourname.github.io 这个网站看到你的博客了！！

7. 设置个人域名
现在你的个人网站的地址是 yourname.github.io，如果觉得这个网址逼格不太够，这就需要你设置个人域名了。但是需要花钱。

注册一个阿里云账户,在阿里云上买一个域名，我买的是 fangzh.top，各个后缀的价格不太一样，比如最广泛的.com就比较贵，看个人喜好咯。

你需要先去进行实名认证,然后在域名控制台中，看到你购买的域名。

点解析进去，添加解析。

登录GitHub，进入之前创建的仓库，点击settings，设置Custom domain，输入你的域名fangzh.top

然后在你的博客文件source中创建一个名为CNAME文件，不要后缀。写上你的域名。

最后，在gitbash中，输入

hexo clean
hexo g
hexo d
过不了多久，再打开你的浏览器，输入你自己的域名，就可以看到搭建的网站啦！

接下来你就可以正式开始写文章了。

hexo new newpapername
然后在source/_post中打开markdown文件，就可以开始编辑了。当你写完的时候，再

hexo clean
hexo g
hexo d


第二部分
hexo的基本配置，更换主题，实现多终端工作，以及在coding page部署实现国内外分流。

1. hexo基本配置


在文件根目录下的_config.yml，就是整个hexo框架的配置文件了。可以在里面修改大部分的配置。详细可参考官方的配置描述。

网站
参数描述title网站标题subtitle网站副标题description网站描述author您的名字language网站使用的语言timezone网站时区。Hexo 默认使用您电脑的时区。时区列表。比如说：America/New_York, Japan, 和 UTC 。

其中，description主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。author参数用于主题显示文章的作者。



网址
参数描述url网址root网站根目录permalink文章的 永久链接 格式permalink_defaults永久链接中各部分的默认值

在这里，你需要把url改成你的网站域名。

permalink，也就是你生成某个文章时的那个链接格式。

比如我新建一个文章叫temp.md，那么这个时候他自动生成的地址就是http://yoursite.com/2018/09/05/temp。

以下是官方给出的示例，关于链接的变量还有很多，需要的可以去官网上查找 永久链接 。

参数结果:year/:month/:day/:title/2013/07/14/hello-world:year-:month-:day-:title.html2013-07-14-hello-world.html:category/:titlefoo/bar/hello-world



再往下翻，中间这些都默认就好了。



theme: landscape
​
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
​
theme就是选择什么主题，也就是在theme这个文件夹下，在官网上有很多个主题，默认给你安装的是lanscape这个主题。当你需要更换主题时，在官网上下载，把主题的文件放在theme文件夹下，再修改这个参数就可以了。



接下来这个deploy就是网站的部署的，repo就是仓库(Repository)的简写。branch选择仓库的哪个分支。这个在之前进行github page部署的时候已经修改过了，不再赘述。而这个在后面进行双平台部署的时候会再次用到。



Front-matter
Front-matter 是文件最上方以 --- 分隔的区域，用于指定个别文件的变量，举例来说：

title: Hello World
date: 2013/7/13 20:46:25
---
下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

参数描述layout布局title标题date建立日期updated更新日期comments开启文章的评论功能tags标签（不适用于分页）categories分类（不适用于分页）permalink覆盖文章网址



其中，分类和标签需要区别一下，分类具有顺序性和层次性，也就是说 Foo, Bar 不等于 Bar, Foo；而标签没有顺序和层次。

categories:
- Diary
tags:
- PS3
- Games
layout（布局）
当你每一次使用代码

hexo new paper
它其实默认使用的是post这个布局，也就是在source文件夹下的_post里面。

Hexo 有三种默认布局：post、page 和 draft，它们分别对应不同的路径，而您自定义的其他布局和 post 相同，都将储存到 source/_posts 文件夹。

布局路径postsource/_postspagesourcedraftsource/_drafts

而new这个命令其实是：

hexo new [layout] <title>
只不过这个layout默认是post罢了。



page
如果你想另起一页，那么可以使用

hexo new page board
系统会自动给你在source文件夹下创建一个board文件夹，以及board文件夹中的index.md，这样你访问的board对应的链接就是http://xxx.xxx/board

draft
draft是草稿的意思，也就是你如果想写文章，又不希望被看到，那么可以

hexo new draft newpage
这样会在source/_draft中新建一个newpage.md文件，如果你的草稿文件写的过程中，想要预览一下，那么可以使用

hexo server --draft
在本地端口中开启服务预览。



如果你的草稿文件写完了，想要发表到post中，

hexo publish draft newpage
就会自动把newpage.md发送到post中。

2. 更换主题
到这一步，如果你觉得默认的landscape主题不好看，那么可以在官网的主题中，选择你喜欢的一个主题进行修改就可以啦。
这里有200多个主题可以选。不过最受欢迎的就是那么几个，比如NexT主题，非常的简洁好看，大多数人都选择这个，关于这个的教程也比较多。不过我选择的是hueman这个主题，好像是从WordPress移植过来的.


直接在github链接上下载下来，然后放到theme文件夹下就行了，然后再在刚才说的配置文件中把theme换成那个主题文件夹的名字，它就会自动在theme文件夹中搜索你配置的主题。



而后进入hueman这个文件夹，可以看到里面也有一个配置文件_config.xml，貌似它默认是_config.xml.example，把它复制一份，重命名为_config.xml就可以了。这个配置文件是修改你整个主题的配置文件。

menu（菜单栏）
也就是上面菜单栏上的这些东西。

其中，About这个你是找不到网页的，因为你的文章中没有about这个东西。如果你想要的话，可以执行命令

hexo new page about
它就会在根目录下source文件夹中新建了一个about文件夹，以及index.md，在index.md中写上你想要写的东西，就可以在网站上展示出来了。

如果你想要自己再自定义一个菜单栏的选项，那么就

hexo new page yourdiy
然后在主题配置文件的menu菜单栏添加一个 Yourdiy : /yourdiy，注意冒号后面要有空格，以及前面的空格要和menu中默认的保持整齐。然后在languages文件夹中，找到zh-CN.yml，在index中添加yourdiy: '中文意思'就可以显示中文了。



customize(定制)
在这里可以修改你的个人logo，默认是那个hueman，在source/css/images文件夹中放入自己要的logo，再改一下url的链接名字就可以了。

favicon是网站中出现的那个小图标的icon，找一张你喜欢的logo，然后转换成ico格式，放在images文件夹下，配置一下路径就行。

social_links ，可以显示你的社交链接，而且是有logo的。

tips:

在这里可以添加一个rss功能，也就是那个符号像wifi一样的东西。

添加RSS
1. 什么是RSS？

RSS也就是订阅功能，你可以理解为类似与订阅公众号的功能，来订阅各种博客，杂志等等。

2. 为什么要用RSS？

就如同订阅公众号一样，你对某个公众号感兴趣，你总不可能一直时不时搜索这个公众号来看它的文章吧。博客也是一样，如果你喜欢某个博主，或者某个平台的内容，你可以通过RSS订阅它们，然后在RSS阅读器上可以实时推送这些消息。现在网上的垃圾消息太多了，如果你每一天都在看这些消息中度过，漫无目的的浏览，只会让你的时间一点一点的流逝，太不值得了。如果你关注的博主每次都发的消息都是精华，而且不是每一天十几条几十条的轰炸你，那么这个博主就值得你的关注，你就可以通过RSS订阅他。

在我的理解中，如果你不想每天都被那些没有质量的消息轰炸，只想安安静静的关注几个博主，每天看一些有质量的内容也不用太多，那么RSS订阅值得你的拥有。

3. 添加RSS功能

先安装RSS插件

npm i hexo-generator-feed
而后在你整个项目的_config.yml中找到Extensions，添加：

# Extensions
## Plugins: https://hexo.io/plugins/
#RSS订阅
plugin:
- hexo-generator-feed
#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20
这个时候你的RSS链接就是 域名/atom.xml了。

所以，在主题配置文件中的这个social links，开启RSS的页面功能，这样你网站上就有那个像wifi一样符号的RSS logo了，注意空格。

rss: /atom.xml
4. 如何关注RSS？

首先，你需要一个RSS阅读器，在这里我推荐inoreader，宇宙第一RSS阅读器，而且中文支持的挺好。不过它没有PC端的程序，只有网页版，chrome上有插件。在官网上用google账号或者自己注册账号登录，就可以开始你的关注之旅了。

每次需要关注某个博主时，就点开他的RSS链接，把链接复制到inoreader上，就能关注了，当然，如果是比较大众化的很厉害的博主，你直接搜名字也可以的，比如每个人都非常佩服的阮一峰大师，直接在阅读器上搜索阮一峰，应该就能出来了。

我关注的比如，阮一峰的网络日志，月光博客，知乎精选等，都很不错。当然，还有我！！赶快关注我吧！你值得拥有：http://fangzh.top/atom.xml

在安卓端，inoreader也有下载，不过因为国内google是登录不了的，你需要在inoreader官网上把你的密码修改了，然后就可以用账户名和密码登录了。

在IOS端，没用过，好像是reader 3可以支持inoreader账户，还有个readon也不错，可以去试试。

widgets(侧边栏)
侧边栏的小标签，如果你想自己增加一个，比如我增加了一个联系方式，那么我把communication写在上面，在zh-CN.yml中的sidebar，添加communication: '中文'。

然后在hueman/layout/widget中添加一个communicaiton.ejs，填入模板：

<% if (site.posts.length) { %>
    <div class="widget-wrap widget-list">
        <h3 class="widget-title"><%= __('sidebar.communiation') %></h3>
        <div class="widget">
            <!--这里添加你要写的内容-->
        </div>
    </div>
<% } %>

search(搜索框)
默认搜索框是不能够用的，

you need to install hexo-generator-json-content before using Insight Search
它已经告诉你了，如果想要使用，就安装这个插件。

3. git分支进行多终端工作
问题来了，如果你现在在自己的笔记本上写的博客，部署在了网站上，那么你在家里用台式机，或者实验室的台式机，发现你电脑里面没有博客的文件，或者要换电脑了，最后不知道怎么移动文件，怎么办？

在这里我们就可以利用git的分支系统进行多终端工作了，这样每次打开不一样的电脑，只需要进行简单的配置和在github上把文件同步下来，就可以无缝操作了。

机制
机制是这样的，由于hexo d上传部署到github的其实是hexo编译后的文件，是用来生成网页的，不包含源文件。

也就是上传的是在本地目录里自动生成的.deploy_git里面。

其他文件 ，包括我们写在source 里面的，和配置文件，主题文件，都没有上传到github

所以可以利用git的分支管理，将源文件上传到github的另一个分支即可。

上传分支
首先，先在github上新建一个hexo分支。然后在这个仓库的settings中，选择默认分支为hexo分支（这样每次同步的时候就不用指定分支，比较方便）。
然后在本地的任意目录下，打开git bash，

git clone git@github.com:ZJUFangzh/ZJUFangzh.github.io.git
将其克隆到本地，因为默认分支已经设成了hexo，所以clone时只clone了hexo。

接下来在克隆到本地的ZJUFangzh.github.io中，把除了.git 文件夹外的所有文件都删掉

把之前我们写的博客源文件全部复制过来，除了.deploy_git。这里应该说一句，复制过来的源文件应该有一个.gitignore，用来忽略一些不需要的文件，如果没有的话，自己新建一个，在里面写上如下，表示这些类型文件不需要git：

.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
注意，如果你之前克隆过theme中的主题文件，那么应该把主题文件中的.git文件夹删掉，因为git不能嵌套上传，最好是显示隐藏文件，检查一下有没有，否则上传的时候会出错，导致你的主题文件无法上传，这样你的配置在别的电脑上就用不了了。

而后

git add .
git commit –m "add branch"
git push 
这样就上传完了，可以去你的github上看一看hexo分支有没有上传上去，其中node_modules、public、db.json已经被忽略掉了，没有关系，不需要上传的，因为在别的电脑上需要重新输入命令安装 。

这样就上传完了。



更换电脑操作
一样的，跟之前的环境搭建一样，

安装git
sudo apt-get install git
设置git全局邮箱和用户名
git config --global user.name "yourgithubname"
git config --global user.email "yourgithubemail"
设置ssh key
ssh-keygen -t rsa -C "youremail"
#生成后填到github和coding上（有coding平台的话）
#验证是否成功
ssh -T git@github.com
ssh -T git@git.coding.net #(有coding平台的话)
安装nodejs
sudo apt-get install nodejs
sudo apt-get install npm
安装hexo
sudo npm install hexo-cli -g
但是已经不需要初始化了，

直接在任意文件夹下，

git clone git@………………
然后进入克隆到的文件夹：

cd xxx.github.io
npm install
npm install hexo-deployer-git --save
生成，部署：

hexo g
hexo d


然后就可以开始写你的新博客了

hexo new newpage


Tips:

不要忘了，每次写完最好都把源文件上传一下
git add .
git commit –m "xxxx"
git push 
如果是在已经编辑过的电脑上，已经有clone文件夹了，那么，每次只要和远端同步一下就行了
git pull

第三部分
hexo添加各种功能，包括搜索的SEO，阅读量统计，访问量统计和评论系统等。

这一部分参考了: visugar.com这里面说的很详细了。

1. SEO优化
推广是很麻烦的事情，怎么样别人才能知道我们呢，首先需要让搜索引擎收录你的这个网站，别人才能搜索的到。那么这就需要SEO优化了。

SEO是由英文Search Engine Optimization缩写而来， 中文意译为“搜索引擎优化”。SEO是指通过站内优化比如网站结构调整、网站内容建设、网站代码优化等以及站外优化。
百度seo
刚建站的时候是没有搜索引擎收录我们的网站的。可以在搜索引擎中输入site:<域名>

来查看一下。



1. 登录百度站长平台添加网站

登录百度站长平台，在站点管理中添加你自己的网站。

验证网站有三种方式：文件验证、HTML标签验证、CNAME验证。

第三种方式最简单，只要将它提供给你的那个xxxxx使用CNAME解析到http://xxx.baidu.com就可以了。也就是登录你的阿里云，把这个解析填进去就OK了。

2. 提交链接

我们需要使用npm自动生成网站的sitemap，然后将生成的sitemap提交到百度和其他搜索引擎

npm install hexo-generator-sitemap --save     
npm install hexo-generator-baidu-sitemap --save
这时候你需要在你的根目录下_config.xml中看看url有没有改成你自己的：








重新部署后，就可以在public文件夹下看到生成的sitemap.xml和baidusitemap.xml了。

然后就可以向百度提交你的站点地图了。

这里建议使用自动提交。

自动提交又分为三种：主动推送、自动推送、sitemap。

可以三个一起提交不要紧，我选择的是后两种。

自动推送：把百度生成的自动推送代码，放在主题文件/layout/common/head.ejs的适当位置，然后验证一下就可以了。
sitemap：把两个sitemap地址，提交上去，看到状态正常就OK了。
google的SEO


流程一样，google更简单，而且收录更快，进入google站点地图，提交网站和sitemap.xml，就可以了。

如果你这个域名在google这里出了问题，那你就提交 http://yourname.github.io，这个链接，效果是一样的。

不出意外的话一天内google就能收录你的网站了。

3. 添加百度统计


百度统计可以在后台上看到你网站的访问数，浏览量，浏览链接分布等很重要的信息。所以添加百度统计能更有效的让你掌握你的网站情况。

百度统计，注册一下，这里的账号好像和百度账号不是一起的。








