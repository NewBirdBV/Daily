------
# 2017/5/15
* Homebrew简介：<br/>
	Homebrew简称brew，是Mac OSX上的软件包管理工具，能在Mac中方便的安装软件或者卸载软件，可以说Homebrew就是mac下的apt-get、yum神器。
* Homebrew常用操作：<br/>
	* brew search 软件名
	* brew install 软件名
	* brew remove 软件名
* iTerm:<br/>
	* 一款 os X平台的终端管理工具.
* ssh key的生成<br/>
	1. 先查看本地有无 ssh key:<br/>
    		$ cd ~/.ssh
		$ ls
	2. 创建一个ssh key:<br/>
		$ ssh-keygen -t rsa -C "your_email@example.com"
	3. 输入文件名.按下 enter键使用默认的文件名.
	4. 输入 push文件时候要用的密码.
	5. 添加到自己的 github 账号里.
	
---------

# 2017/5/16
* webpack,npm,react 开发框架搭建<br/>
	* webpack全局安装时可能要在命令前加入 'sudo',否则会安装失败.如下:<br />
	<code>sudo npm install webpack -g</code>
	* 在 package.json 中 devDependencies 里面的插件只用于开发环境，不用于生产环境，而 dependencies  是需要发布到生产环境的。
	* 卸载开发环境里的包
	<code>npm uninstall packageName --save-dev</code>
	* 在使用webpack+npm+react的开发模式种中，难点在于webpack.config.js的配置:<br/>
	     >
	     1.路径的配置必须为绝对路径，但相对路径也不会报错。比较常用的配置方法如下：<br/>
		>`var path = require('path');`
		>	
		>打包输出：`output:{
        			path:path.resolve(__dirname, 'dist/assets'),
        			filename:'index.js'
    			},`
		>
	     2.在使用webpack时，需要添加HtmlWebpackPlugin组件：<br/>
             >`var HtmlWebpackPlugin = require('html-webpack-plugin');`
	     >
	     >组件配置:
	     >`plugins: [
        			new HtmlWebpackPlugin({
            				template: __dirname + "/src/index.html"//new 一个这个插件的实例，并传入相关的参数
        			})
    			]`
	

	
