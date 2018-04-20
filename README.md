---
title: 【笔记】webpack
date: 2018-04-20 13:53:22
tags: webpack
---
# 如何在项目中引入webpack #

## webpack是什么 ##
*（webpack就是`npx webpack`,报错，`npm install [module name]`，`npx webpack`再报错，google报错原因，再`npx webpack`的一个循环）*

/////////////////////////////////////////////////////////////////////////////////![](https://i.imgur.com/V7Ep0cf.gif)/////////////////////////////////////////////////////////////////////


webpack可以将项目中已经模块化的各个小JavaScript文件和CSS文件打包成一个JavaScript文件（bundle.js）,然后在html中直接引用这个bundle.js就可以了，同时他也可以加载各种预处理器（例如sass,babel）对代码进行处理

将
![](https://i.imgur.com/QABP04N.jpg)变为![](https://i.imgur.com/9zoAejV.jpg)

## 使用webpack的步骤 ##

（以后也许会有不同，仅供自己学习参考）

1.在项目的根目录下运行

	$ npm init

生成一个package.json文件，里面会包含项目的信息和之后安装的模块。

![](https://i.imgur.com/jtOnxc7.jpg)

其中的dependencies会用于生产环境，devDependencies只用于开发阶段。

2.根目录运行

	$ npm install webpack webpack-cli --save-dev
会自动生成一个node_modules文件夹，webpack和之后的下载的模块都存在于这个文件中

![](https://i.imgur.com/Kf1Ffj0.jpg)

3.根目录创建webpack.config.js文件并写入下面的代码，用于webpack的配置。

	const path = require('path');

	module.exports = {
	  entry: './src/index.js',    //webpack需要一个唯一的入口js文件，src目录是自行创建的专用于存放原始代码的目录
	  output: {
	    filename: 'bundle.js',    //bundle.js是打包后输出的js文件
	    path: path.resolve(__dirname, 'dist') //这里用来设置输出的位置。
	  }
	};
4.使用webpack



- src中的分模块js文件变为下面的样式



		export default function(){
			//你的js内容
		} //等于是将代码包裹在一个匿名函数中输出出去。

- 在唯一入口index.js中使用import引入所有的小文件，像这样

![](https://i.imgur.com/pblS3w2.jpg)


这个形式类似立即执行函数。

- 然后在命令行使用`npx webpack`就可以打包成bundle.js了。

5.使用各种预处理器或者转换器。

- google 搜索 wenpack + 你要的module的名字。

	按照文档指示下载，重点是在webpack.config.js中的export中添加module属性，基本就是各种不同的loader

![](https://i.imgur.com/TgTWjxz.jpg)

**一定要按照文档一步步来，报错就google，肯定没问题的。**

其中的mode属性可以设置你输出的bundle.js是开发用还是生产用，就是是否被压缩成min版本。