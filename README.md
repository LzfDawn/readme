<p align="center">
  <img width="320" src="https://wpimg.wallstcn.com/ecc53a42-d79b-42e2-8852-5126b810a4c8.svg">
</p>


## 简介（最佳前后端分离式动态权限路由解决方案）

[vue-element]是一个后台集成解决方案，它基于 [vue](https://github.com/vuejs/vue) 和 [element](https://github.com/ElemeFE/element)。它使用了最新的前端技术栈，内置了 i18 国际化解决方案，动态路由，权限验证，提炼了典型的业务模型，提供了丰富的功能组件，它可以帮助你快速搭建企业级中后台产品原型。相信不管你的需求是什么，本项目都能帮助到你。

- [本项目实现了路由动态加载，服务器无状态性，后端可根据实际刷新token鉴权]
- [相关细粒度按钮级别权限建议使用指令方式实现，本项目中暂时没有设计]
- [相关权限表设计可找我获取]
## 前序准备

你需要在本地安装 [node](http://nodejs.org/) 和 [git](https://git-scm.com/)。本项目技术栈基于 [ES6](http://es6.ruanyifeng.com/)、[vue](https://cn.vuejs.org/index.html)、[vuex](https://vuex.vuejs.org/zh-cn/)、[vue-router](https://router.vuejs.org/zh-cn/) 、[axios](https://github.com/axios/axios) 和 [element-ui](https://github.com/ElemeFE/element)，所有的请求数据都使用[Mock.js](https://github.com/nuysoft/Mock)模拟、[ESLint](https://eslint.org/docs/rules/no-multiple-empty-lines)规范js开发，提前了解和学习这些知识会对使用本项目有很大的帮助。

1: 本项目是基于springBoot2.0.4 开发，jdk8，shiro和jwt做权限和鉴权，前期开发准备idea 下载vue、es6插件，本地安装nodejs和vue-cli。
<br/><br/>
2: 本项目的guarantee_loan_foreground可以是单独的一个文件夹，可以分离，可以整合到一起。 注意：如果分离开来需要修改文件夹config的index.js文件中‘index’和‘assetsRoot’，‘productionSourceMap’是否生成map文件，上线打包建议修改false,减小浏 览器加载大小； 如果出错运行‘npm install’,然后运行‘npm run dev’
<br/><br/>
3：相关的前端 原版是，可以下载运行使用相关模板
git clone https://github.com/PanJiaChen/vue-element-admin.git
<br/>
相关命令
<br/>
npm install
<br/>
建议不要用 cnpm 安装 会有各种诡异的bug 可以通过如下操作解决 npm 下载速度慢的问题
<br/>
npm install --registry=https://registry.npm.taobao.org
<br/>
启动服务
<br/>
npm run dev




 <p align="center">
  <img width="900" src="https://wpimg.wallstcn.com/a5894c1b-f6af-456e-82df-1151da0839bf.png">
</p>

## 开发
一：
<strong>权限
 <br/>
 1、请求认证的流程其实和登录认证流程是比较相似的，因为我们的服务是无状态的，所以每次请求带来token，我们就是做了一次登录操作。
 JwtAuthFilter
 首先我们先从入口的Filter开始。从AuthenticatingFilter继承，重写isAccessAllow方法，方法中调用父类executeLogin()。父类的这个方法首先会createToken()，然后调用shiro的Subject.login()方法。
  <br/><br/>
 2、注意鉴权使用的盐值需要存储到缓存或者数据库中，前台退出后要删除。
  <br/><br/>
 3、JWT Token刷新
   前面的Filter里面还有一个逻辑，就是如果用户这次的token校验通过后，我们还会顺便看看token要不要刷新，如果需要刷新则将新的token放到header里面。
   这样做的目的是防止token丢了之后，别人可以拿着一直用。我们这里是固定时间刷新。安全性要求更高的系统可能每次请求都要求刷新，或者是每次POST，PUT等修改数据的请求后必须刷新。
    <br/><br/>
 4、流程图
  <br/>
  <p align="center">
   <img width="600" src="http://upload-images.jianshu.io/upload_images/13282795-0e7d8ee5d4af35e3.png">
 </p>
 <br/><br/>
5、后端权限：
  在UserController接口具体逻辑getUser()实现
   <br/>
   前端在permission.js实现，具体看文件代码；
  <br/>
5、开发工具 idea 版本在2019.2.1以上：

## 前端目录结构

├── build                      # 构建相关
├── mock                       # 项目mock 模拟数据
├── plop-templates             # 基本模板
├── public                     # 静态资源
│   │── favicon.ico            # favicon图标
│   └── index.html             # html模板
├── src                        # 源代码
│   ├── api                    # 所有请求
│   ├── assets                 # 主题 字体等静态资源
│   ├── components             # 全局公用组件
│   ├── directive              # 全局指令
│   ├── filters                # 全局 filter
│   ├── icons                  # 项目所有 svg icons
│   ├── lang                   # 国际化 language
│   ├── layout                 # 全局 layout
│   ├── router                 # 路由
│   ├── store                  # 全局 store管理
│   ├── styles                 # 全局样式
│   ├── utils                  # 全局公用方法
│   ├── vendor                 # 公用vendor
│   ├── views                  # views 所有页面
│   ├── App.vue                # 入口页面
│   ├── main.js                # 入口文件 加载组件 初始化等
│   └── permission.js          # 权限管理
├── tests                      # 测试
├── .env.xxx                   # 环境变量配置
├── .eslintrc.js               # eslint 配置项
├── .babelrc                   # babel-loader 配置
├── .travis.yml                # 自动化CI配置
├── vue.config.js              # vue-cli 配置
├── postcss.config.js          # postcss 配置
└── package.json               # package.json

## 前端目录结构
安装依赖
npm install

 建议不要用 cnpm 安装 会有各种诡异的bug 可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

本地开发 启动项目
npm run dev

## 打包
-前端项目guarantee_loan_foreground 打包上线：npm run build:prod
-会生成dist文件夹，里面是打包压缩好的文件。
-后端项目正式环境打包mvn clean package -P prod 
  
## 
<br/><br/>
Copyright (c) 2017-present LZF
