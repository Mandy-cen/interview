title: uni-app项目搭建+云打包
date: 2020-07-21 17:50:55
tags:
    - uni-app
---
---
#背景
uni-app 是一个使用 Vue.js 开发跨平台应用的前端框架，开发者编写一套代码，可编译到iOS、Android、H5、小程序等多个平台。
#项目搭建

下载官方推荐编辑器：[HBuilderX][1] 
HBuilderX是通用的前端开发工具，但为uni-app做了特别强化。

##创建uni-app
   - 在点击工具栏里的文件 -> 新建 -> 项目：
  ![新建项目][2]  
  选择uni-app类型，输入工程名，选择模板，点击创建，即可成功创建。
   - uni-app自带的模板有 Hello uni-app ，是官方的组件和API示例。还有一个重要模板是 uni ui项目模板，日常开发推荐使用该模板，已内置大量常用组件。
  ![创建项目][3]
  
   - 运行uni-app
   （1）浏览器运行：进入hello-uniapp项目，点击工具栏的运行 -> 运行到浏览器 -> 选择浏览器，即可在浏览器里面体验uni-app 的 H5 版。
  ![运行项目][4]
   （2）真机运行：连接手机，开启USB调试，进入hello-uniapp项目，点击工具栏的运行 -> 真机运行 -> 选择运行的设备，即可在该设备里面体验uni-app。
  ![dev][5]
    （3）在微信开发者工具里运行：进入hello-uniapp项目，点击工具栏的运行 -> 运行到小程序模拟器 -> 微信开发者工具，即可在微信开发者工具里面体验uni-app。
    ![微信dev][6]
  
    ```
    注意：如果是第一次使用，需要先配置小程序ide的相关路径，才能运行成功。如下图，需在输入框输入微信开发者工具的安装路径。 若HBuilderX不能正常启动微信开发者工具，需要开发者手动启动，然后将uni-app生成小程序工程的路径拷贝到微信开发者工具里面，在HBuilderX里面开发，在微信开发者工具里面就可看到实时的效果。
    ```
    uni-app默认把项目编译到根目录的unpackage目录。
    ![地址配置][7]

## 发布uni-app
- 打包为原生App（云端）
    在HBuilderX工具栏，点击发行，选择原生app-云端打包，如下图：
![云打包][8]
这里打包app需要证书，分为ios和Andorid
[Android平台签名证书(.keystore)生成指南][9]
[iOS证书(.p12)和描述文件(.mobileprovision)证书申请][10]
打包完成之后我们可以到[dcloud开发者中心][11]下载apk文件安装到手机上就可以看到效果了


  [1]: https://www.dcloud.io/hbuilderx.html
  [2]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/create1.png
  [3]: https://img.cdn.aliyun.dcloud.net.cn/uni-app/doc/create.png
  [4]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/run-chrome.png
  [5]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/run-phone.png
  [6]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/uni20190222-1.png
  [7]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/weixin-setting.png
  [8]: https://img-cdn-qiniu.dcloud.net.cn/uniapp/doc/uni20190222-11.png
  [9]: https://ask.dcloud.net.cn/article/35777
  [10]: https://ask.dcloud.net.cn/article/152
  [11]: https://dev.dcloud.net.cn/app/index?type=0