## [全球粮食安青年科学家联盟](https://thefoodsecurity.org/)网站维护指南

### 简介
网站使用的**hexo** + **github** 完成内容编写和项目部署

> **社会仿真学（https://socialsimulation.net）** 类似，hexo类站点维护方式基本一致，仅可能因为采用主题不同有少量差异

[hexo官网](https://hexo.io/)

选择hexo主要原因：

- 建站门槛低，生态发展良好
- 使用markdown语言，可移植性强，兼容性好
- 灵活 不支持的样式需求（如水平居中，垂直居中）可以通过直接写HTML来

> PS: 要实现灵活的样式需求需要具备一定的web前端知识

### 准备工作
#### 项目环境搭建
##### 1.安装git
什么是Git ?

简单来说Git是开源的分布式版本控制系统，用于敏捷高效地处理项目。

从Git官网下载：[Git - Downloading Package](https://git-scm.com/download/win) 现在的机子基本都是64位的，选择64位的安装包，（也可通过[本链接下载Git-2.39.2-64-bit](https://github.com/git-for-windows/git/releases/download/v2.39.2.windows.1/Git-2.39.2-64-bit.exe)）快速下载后安装。
安装成功后在命令行里输入git测试是否安装成功。

![](/images/git-v.png)

若安装失败，参看其他详细的Git安装教程。


##### 2.安装nodejs

Hexo基于Node.js，Node.js下载地址：[Download | Node.js](https://nodejs.org/en/download/) 下载安装包，（也可通过[本链接下载node-v16.19.0-x64](https://nodejs.org/download/release/v16.19.0/node-v16.19.0-x64.msi)）快速下载后安装。
注意安装Node.js会包含环境变量及npm的安装，安装后，检测Node.js是否安装成功，在命令行中输入 `node -v`:

![](/images/node-v.png)

检测npm是否安装成功，在命令行中输入`npm -v` :

![](/images/node-v.png)

##### 3.安装hexo

使用npm命令安装Hexo，输入：
```
npm install -g hexo-cli
```

以上安装成功后，Hexo运行的环境已经全部搭建完成。

> 更多相关详细教程可以参考网上的[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249/)

---

### 项目启动
**全球粮食安青年科学家联盟** 源代码地址[https://github.com/Social-Simulation/thefoodsecurity](https://github.com/Social-Simulation/thefoodsecurity)

> **社会仿真学** 源码地址 [https://github.com/Social-Simulation/socialsimulation](https://github.com/Social-Simulation/socialsimulation)

需要按照依赖的前端npm包，有主项目和主题suka两处

步骤如下：

使用终端运行,

```
git clone https://github.com/Social-Simulation/thefoodsecurity
```

进入主题文件夹
```
cd thefoodsecurity/themes/suka
```

安装主题依赖
```
npm install
```
返回项目文件夹thefoodsecurity
```
cd ../..
```
安装项目依赖
```
npm install
```

上述全部成功后，本地启动项目
```
npm run server
```

打开
**[http://localhost:4000/](http://localhost:4000/)**
即可看到效果

![](/images/npm-run-server.png)

### 编写内容
#### IDE
可以使用微软免费开源的Visual Studio Code[下载地址](https://az764295.vo.msecnd.net/stable/6c3e3dba23e8fadc360aed75ce363ba185c49794/VSCodeUserSetup-x64-1.81.1.exe)或其它自己顺手的编辑器
#### markdown语法
熟悉常用的markdown语法，可参考[http://tool.wdphp.com/markdown.html](http://tool.wdphp.com/markdown.html)，左边输入，右边能看到预览效果

> 看到表格部分即可，剩下的功能一般用不到

hexo需要在本地编写（并预览）markdown格式的文章后，提交到github交由github actions完整自动打包和部署。

#### 项目url生成规则

网站post内容只开放了**About us**（url为/about）、**Events**（url为/events/2023/）、**Initiative**（url为/initiative/）、**Blogs**（即文章列表，url为/blogs/，里面有所属的各个post的访问入口，形如/acticle/national-grain-and-oil-security-initiative/）、**Get Involved**（url为/members/）。

hexo是根据文件（或文件夹）名及其层级来生成访问url的，举例如下：

![](/images/url-rule.png)


#### 其他说明
##### hexo编写内容类型
编写的内容分为page和post两种，平时主要用来写文章的就是post，一般内容固定或者布局、内容与post风格不一致的用page。post是才有category、分页等概念，可以按照category、archive或date列表展示。

> 网站主要是导航上面的页面使用的page，其中Blogs除外，它是category地址，显示分类为posts里面的post。
##### 可视化编辑（不推荐）

hexo没有常规的网站后台所用的编辑器，虽然可以用[hexo语雀插件](https://github.com/x-cold/yuque-hexo)实现将[语雀](https://www.yuque.com/)上编写的内容导出成markdown格式后部署（可参考[]手把手教你打造语雀+Hexo+Github Actions+COS持续集成
(https://blog.csdn.net/qq_32666519/article/details/127594549)），但是实测效果并不好，主要原因：

- 1.语雀编写的内容为html格式，并非所有html格式转为为对应的markdown，部分导出内容会出现小问题，仍需要再次修改
- 2.语雀部分需要开通会员才能正常使用（早期可能无此问题），不宜与其深度绑定。其中最严重的问题是语雀的内容库默认是“私密”的，只有会员才能将其改完“公开”，导致语雀内容中图片导出后在非语雀环境没有权限访问而无法显示。

#### markdown系统样式不满足排版要求时怎么办
arkdown系统样式无法满足要求时需要编写css，css源代码在主题suku内，默认使用的是压缩后的min版本，源代码变更后需要重新编译生成min版，此操作需要使用gulp，需要安装**gulp-cli**

步骤如下：

使用终端运行

进入主题文件夹
```
cd themes/suka
```

安装css打包工具
```
npm install -g gulp-cli
```
打包css
运行`gulp`或`gulp watchCss`(只打包css并且监听css变化后自动打包)

![](/images/gulp-watchCss.png)

### 发布
在编写完内容并通过http://localhost:4000/ 预览满足要求后，提交改动文件至github服务器后，稍等Github Actions完成后即可。

#### github账户
因为现在项目没有自己的服务器，源代码均在[github](https://github.com)上，所以需要申请github并授权后（非授权用户只能查看不能修改）才能发布。

#### 发布流程举例
> 以Visual Studio Code操作为例

比如我们修改了/source/_post/test.md的内容并保存文件
1. 切换至如图所示的tab（左侧第三个图标 Source Control），这里能看到改动的文件，点击每一个文件后还能看到进行了那些改动。

![](/images/git-step1.png)

2. 填写commit信息，并push至服务器
![](/images/git-step2.png)

3. push后，Source Control显示文件为空，同时github上有刚才的提交记录

![](/images/git-step3.png)

![](/images/git-step4.png)

4. 稍等几分钟后github会完成部署

![](/images/git-step5.png)

5. 在网站预览效果

![](/images/git-step6.png)


### 项目结构介绍
##### 主题
本博客基于suka主题（[官网地址](https://theme-suka.skk.moe/docs/)）二次改造后使用
更改了部分样式

因为的业务场景跟单纯的个人博客有所不同，为了将常见博客通用的部分内容隐藏，额外增加了几个front-matter控制开关，默认值为false，避免每篇内容都需要手动关闭

| 名称 | 配置项所在位置 | 默认值 | 说明 |
| --- | --- | --- | --- |
| _showCategoryTitle | 主题配置config.yml | false | 列表页/blogs是否展示当前分类名称 |
| _showCategoryBelong | 各post的front-matter | false |  文章底部是否展示当前文章所属的分类名称 |
| _showPrevNext | 各post的front-matter  | false | 是否文章底部显示上一篇 下一篇 |
| _showAuthor | 各post的front-matter | false | 是否显示作者 |
| _comments | 各post的front-matter | false | 是否显示评论框 hexo官方使用的是comments但是默认值为true，特改用_comments切调整默认值为false |

目前自行实现的功能有：

| 名称 | 配置文件地址 |
| --- | --- |
| 样式、响应式 | themes/suka/src/css/style.css post.css |
| 顶部logo、导航页 | themes/suka/layout/_partial/index-nav.ejs |
| 轮播图 | source/index.md |
| 申请表单提交 | themes/suka/layout/_pages/application.ejs |
| 点击下载次数的统计 | themes/suka/layout/_partial/footer.ejs source/events/index.md |
