网站使用的**hexo** + **github** 完成内容编写和项目部署

[hexo官网](https://hexo.io/)

选择hexo主要原因：

- 建站门槛低，生态发展良好
- 使用markdown语言，可移植性强，兼容性好
- 灵活 不支持的样式需求（如水平居中，垂直居中）可以通过直接写HTML来

> PS: 要实现灵活的样式需求需要具备一定的web前端知识

#### 项目环境搭建 ####
详细教程可以参考网上的[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249/)

**先根据上述教程安装nodejs和hexo**

##### 项目须知 #####
本站源代码地址[https://github.com/shadowprompt/thefoodsecurity](https://github.com/shadowprompt/thefoodsecurity)

需要按照依赖的前端npm包，有主项目和主题suka两处

步骤如下：

使用终端运行,

```
git clone https://github.com/shadowprompt/thefoodsecurity
```

进入主题文件夹
```
cd thefoodsecurity/theme/suka
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

#### css
css源代码在主题suku内，默认使用的是压缩后的min版本，源代码变更后需要重新编译生成min版，此操作需要使用gulp，需要安装**gulp-cli**

步骤如下：

使用终端运行

进入主题文件夹
```
cd theme/suka
```

安装css打包工具
```
npm install -g gulp-cli
```
打包css
运行`gulp`或`gulp watchCss`(只打包css并且监听css变化后自动打包)


#### hexo说明 ####
##### 编写内容类型 #####
编写的内容分为page和post两种，平时主要用来写文章的就是post，一般内容固定或者布局、内容与post风格不一致的用page。post是才有category、分页等概念，可以按照category、archive或date列表展示。

> 本站主要是导航上面的页面使用的page，其中Blogs除外，它是category地址，显示分类为posts里面的post。

##### 编写内容 #####

本站post内容只开放了一个名为*posts*的category列表入口（即导航部分的**Blogs**，url为/blogs/posts/），里面有所属的各个post的访问入口（形如/acticle/xxxx/）

hexo需要在本地编写（并预览）markdown格式的文章后，提交到github交由github actions完整自动打包和部署。

##### 可视化编辑 ####

hexo没有常规的网站后台所用的编辑器，虽然可以用[hexo语雀插件](https://github.com/x-cold/yuque-hexo)实现将[语雀](https://www.yuque.com/)上编写的内容导出成markdown格式后部署（可参考[]手把手教你打造语雀+Hexo+Github Actions+COS持续集成
(https://blog.csdn.net/qq_32666519/article/details/127594549)），但是实测效果并不好，主要原因：

- 1.语雀编写的内容为html格式，并非所有html格式转为为对应的markdown，部分导出内容会出现小问题，仍需要再次修改
- 2.语雀部分需要开通会员才能正常使用（早期可能无此问题），不宜与其深度绑定。其中最严重的问题是语雀的内容库默认是“私密”的，只有会员才能将其改完“公开”，导致语雀内容中图片导出后在非语雀环境没有权限访问而无法显示。

#### 项目结构介绍 ####
##### 主题 #####
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
