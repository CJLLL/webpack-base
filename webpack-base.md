---
date: 2018-11-24 15:22
status: public
title: webpack创建demo示例
---

#初始化npm项目
```
npm init -y
```
#安装
```
npm install webpack webpack-cli --save-dev
```
> 注意:最好安装在当前目录下 全局安装的话可能会有版本问题 使用webpack4.+版本要安装cli

#webpack.config.js配置文件
>在当前项目下新建webpack.config.js文件，用于配置webpack的出入口、loader匹配项等..

##入口(entry)
webpack.config.js
```
module.exports = {
  entry: './src/index.js'
};
//多个入口
module.exports = {
  entry: {
 app : './src/pageOne.js',
 print :  './src/pageTwo.js'
  }
};
```
##出口(output)
```
output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
  //多个出口 根据本身的入口文件名称生成
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].js'
  }
```
>默认的出口是：dist下面的main.js

##loader(我的理解就是编译转换为js认识的东西)
> 注意，loader 能够 import 导入任何类型的模块（例如 .css 文件）
```
module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
```
###加载css
```
npm install --save-dev style-loader css-loader
```
```
{ test: /\.css$/,use: ['style-loader','css-loader'] }
```
###加载图片
```
npm install --save-dev file-loader
```
```
{ test: /\.(png|svg|jpg|gif)$/, use: ['file-loader'] }
```
###加载字体
```
{ test: /\.(woff|woff2|eot|ttf|otf)$/, use: ['file-loader'] }
```
###加载数据
```
npm install --save-dev csv-loader xml-loader
```
```
{ test: /\.(csv|tsv)$/, use: ['csv-loader'] },
{ test: /\.xml$/, use: ['xml-loader'] }
```
###关于postcss添加css前缀问题
>要添加以下依赖项
```
npm install --save-dev  postcss-loader autoprefixer postcss
```

##插件(plugins)
>需要先引用插件

```
const webpack = require('webpack'); // 用于访问内置插件
```
>再去配置插件

```
plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
```
###清理 /dist 文件夹
```
npm install clean-webpack-plugin --save-dev
```
```
const CleanWebpackPlugin = require('clean-webpack-plugin')
```
```
plugins: [
      new CleanWebpackPlugin(['dist'])
    ],
```

##模式(mode)
```
mode: 'production'
//只有两种模式
开发：development 产品：production
```

##使用webpack-dev-server
>webpack-dev-server为我们提供一个简单的web服务器 修改后可以自动生成文件 自动刷新页面






