## 一、vue-cli 工程技术集合介绍
### 问题一：构建vue-cli工程都用到了那些技术，他们的作用是什么？
1、vue.js: vue-cli工程的核心，主要特点是双向数据绑定和组件系统
2、vue-router：vue官方推荐使用的路由框架
3、vuex：专门为vue.ja应用项目开发状态管理器，主要用于维护vue组件间共用的一些变量和方法
4、axios：用于发起get、post等http请求，基于Promise设计
5、vux：专门为vue设计的一款移动端的UI
6、创建emit.js文件，用于vue时间机制的管理
7、webpack：模块加载和vue-cli工程打包器

### 问题二：vue-cli工程常用的命令有哪些
`npm install` - 下载node_modules资源包
`npm run dev` - 开发环境的npm命令
`npm run build` - 生成生产环境部署资源的npm命令
`npm run build --report` - 用于查看vue-cli生产环境部署资源文件大小的npm命令

