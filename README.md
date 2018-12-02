# vueDemo
我的第一个vue demo

新版vue-cli运行旧版配置：
https://www.cnblogs.com/chen-cong/p/8001352.html

新版本配置webpack.dev.conf.js进行本地数据访问，在const portfinder = require(‘portfinder’)后添加
const express = require('express')
const app = express()   //创建express应用程序
var appData = require('../data.json')//加载本地数据文件
var seller = appData.seller//获取对应的本地数据
var goods = appData.goods
var ratings = appData.ratings
var apiRoutes = express.Router()  // 获取一个 express 的路由实例
app.use('/api', apiRoutes)

其中，app.use是express“调用中间件的方法”。所谓“中间件（middleware），就是处理HTTP请求的函数，用来完成各种特定的任务，比如检查用户是否登录、分析数据、以及其他在需要最终将数据发送给用户之前完成的任务。”。这是阮一峰文章的原话。

简而言之，app.use() 里面使用的参数，主要是函数。但这个使用，并不是函数调用，而是使能的意思。当用户在浏览器发出请求的时候，这部分函数才会启用，进行过滤、处理。

然后在下面找到devServer,在里面添加
before(app) {
  app.get('/api/seller', (req, res) => {
    res.json({
      errno: 0,
      data: seller
    })//接口返回json数据，上面配置的数据seller就赋值给data请求后调用
  }),
  app.get('/api/goods', (req, res) => {
    res.json({
      errno: 0,
      data: goods
    })
  }),
  app.get('/api/ratings', (req, res) => {
    res.json({
      errno: 0,
      data: ratings
    })
  })
}
本地data.json数据放在根目录下与index.js同级,重行执行npm run dev,输入  localhost:8080/api/seller即可

