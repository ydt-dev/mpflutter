# reduce-loader

## 介绍

一个用于代码精简的 webpack loader，在小程序场景下构建可以去除代码中不需要的依赖。

## 安装

```
npm install --save-dev reduce-loader
```

## 使用

webpack 配置：

```js
const webpack = require('webpack')

module.exports = {
    // ... 其他配置
    plugins: [
        new webpack.DefinePlugin({
            'process.env.isMiniprogram': true, // 注入环境变量，用于业务代码判断
        }),
        // ... 其他插件
    ],
}

```

业务代码：

```js
import Header from '../common/Header.vue' // 正常 import
import Footer from 'reduce-loader!../common/Footer.vue' // 在 process.env.isMiniprogram 为 true 的情况下，import 进来的 Footer 是一个空对象
import 'reduce-loader!./web' // 在 process.env.isMiniprogram 为 true 的情况下，import 进来的是一个空串
```
