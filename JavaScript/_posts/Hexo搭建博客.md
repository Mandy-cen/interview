---
title: 使用Hexo+hexo-theme-matery搭建一个属于自己的博客
date: 2019-08-24 16:27:55
tags:
    - Hexo
    - hexo-theme-matery
---


最近无意发现Hexo博客框架，[官网](https://hexo.io/zh-cn/docs/)介绍Hexo是一个快速、简洁且高效的博客框架。想着可以利用Hexo+hexo-theme-matery搭建一个博客，用来记录自己的所学到的知识。

### 1. 安装 Hexo

`$ npm install -g hexo-cli`

### 2. 建站

安装 Hexo 完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

`$ hexo init <folder>`
`$ cd <folder>`
`$ npm install`

新建完成后，指定文件夹的目录如下：
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

启动服务
`$ hexo server`
或者
`$ hexo s`
默认情况下，访问网址为： http://localhost:4000/
选项	描述
-p,     --port	重设端口
-s,     --static	只使用静态文件
-l,     --log	启动日记记录，使用覆盖记录格式


### 3. 配置
hexo相关的配置都放在根目录 _config.yml 里面, 里面的配置都写得很简明。

### 4. 切换主题
hexo初始化之后默认的主题是landscape，如果想要切换主题， 可以将提前下载好的主题放在 themes 文件夹内。我个人比较喜欢 [typora-vue-theme](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md) 这个主题，然后修改根目录的 _config.yml 文件，找到对应的 theme , 把theme的值改为对应的主题的文件夹名称就可以了

### 5. 上传到github
5.1. 创建仓库
新建一个名为你的用户名.github.io的仓库。
例如，如果你的github用户名是test，那么你就新建test.github.io的仓库，后面访问的博客地址就是 http://test.github.io 

5.2 部署
安装 hexo-deployer-git
`$ npm install hexo-deployer-git --save`

修改配置。
在_config.yml文件中，找到Deployment，然后按照如下修改

```yaml
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: master
```

1) 执行以下命令生成博客的静态页面
`$ hexo generate`
或者 `$ hexo g`

2) 执行以下命令将我们生成的博客静态页面上传到GitHub
`$ hexo deploy`
或者 `$ hexo d`

3) 打开浏览器访问 username.github.io 即可访问我们刚部署到Github上的博客

### 6. 备份hexo代码

对于一个开发人员来说保存和备份代码是非常重要的。使用hexo在githut上搭建博客，仓库里只有生成网页的静态文件，是没有hexo的源文件的，所以如果要换电脑开发写博客的话就会很麻烦。这时我们可以利用分支来备份代码，master分支上保存的是hexo生成的静态文件（上面第五步的deploy配置分支是master），新建hexo分支来备份源文件
    
首先在本地仓库下的master分支下创建个hexo分支, 后面修改项目提交都是提交到这个分支上
 ![](https://raw.githubusercontent.com/Mandy-cen/Mandy-cen.github.io/hexo/themes/matery/source/images/20190829155537.png)   

执行 `git add, git commit -m "初始化项目", git push origin hexo` 这样hexo分支下就备份了源代码了

如果想发布新文章到博客上，直接执行hexo g -d 就可以部署到github上了
### 7. 总结常用命令

1) 模版
```yaml
    hexo new "postName" #新建文章
    hexo new page "pageName" #新建页面
    hexo new photo "My Gallery"
```

2) 草稿
```yaml
    hexo publish [layout] <title>
```

3) 服务器
```yaml
    hexo server #Hexo 会监视文件变动并自动更新，您无须重启服务器。
    hexo server -s #静态模式
    hexo server -p 4400 #更改端口
    hexo server -i 192.168.3.10 #自定义 IP
    
    hexo clean #清除缓存 网页正常情况下可以忽略此条命令
    hexo g #生成静态网页
    hexo d #部署 #可与hexo g合并为 hexo d -g
```

4) hexo
```yaml
    npm install hexo -g #安装  
    npm update hexo -g #升级  
    hexo init #初始化
```
