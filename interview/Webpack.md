# Webpack

webpack是一个模块打包工具,通过入口文件分析依赖,递归找到所有文件后打包.
通过依赖分析还可以进行模块代码分割.

## 基本功能

- 代码转换: ts转成js,新版本js转成低版本js并加入polyfill
- 文件压缩: 可以对js,图片,css文件之类的进行代码压缩
- 代码分割: 通过依赖分析,可以把代码文件按模块分割.懒加载或者按需加载.
- devServer: 本地开发的时候可以代理接口,热重载项目,提高开发速度.

### 热重载原理

![hot-reload](images/hotreload-flow.jpg)

流程:

1. webpack进入watch模式,对当前文件打包后监控文件变化,进行增量打包
2. web-dev-server开启,开始与webpack进行交互.比如webpack监控到文件变化进行打包后通知web-dev-server.
3. web-dev-server通过sockjs与客户端建立连接(websocket),当监控到文件改变的时候发送数据让客户端知道.
4. web-dev-server发送文件跟新的哈希值给客户端知道,客户端根据哈希值请求更新之后的文件.
5. 客户端获取文件之后,判断是否需要重新刷新页面,如果是Vue等框架会对UI组件重新渲染,这样就避免了页面刷新.

## 与grunt、gulp的不同

都是前端的构建工具,早起的时候grunt、gulp相对流行

不同点:
  
- grunt、gulp是给予任务和流的,开发者需要自行定义一系列任务.webpack则通过配置文件,查找入口文件后分析依赖,最后完成整个项目的打包

## 相同工具

- webpack
- rollup
- parcel

区别:

- webpack是对整个前端项目进行打包构建的工具
- rollup通常用来对某个基础库的打包,vue、react等
- parcel比较新,时刻用来打包简单的项目

## 常见loader

loader | 作用
---|---
file-loader | 把一些静态文件(比如json),统一打包到一个文件夹
url-loader | 与file-loader类似,但是文件比较小的时候,可以打包成base64注入到代码内部
source-map-loader | 加载额外的source-map文件
image-loader | 处理图片文件,压缩
babel-loader | 转换js文件,比如es6转换成es5
css-loader | 加载css文件,对css进行模块化、压缩等操作
style-loader | 对css-loader的文件⃣以style标签插入到html文件中
eslint-loader | 利用eslint规范js代码

## 常见plugin

plugin | 作用
---|---
define-plugin | 定义环境变量
commons-chunk-plugin | 提取公共代码
uglifyjs-webpack-plugin | 压缩js代码
mini-css-extract-plugin | 分离css文件
html-webpack-plugin | 为html引入外部资源,生成index.html入口文件

## 优化前端新能

- 压缩代码,减少包大小
- tree shaking,减少死代码,减少包大小
- 缓存比较少更改的代码
- 提取公共代码,减少整体的包大小

## 提高webpack构建速度

- 通过`externals`配置,提起常用库,但不对其操作
- 利用`DllPlugin`和`DllReferencePlugin`预编译不会更改的包
- 使用`Happypack`利用多线程加速变异
- 使用`webpack-uglify-parallel`提高压缩js代码的速度

