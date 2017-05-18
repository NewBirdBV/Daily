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
		1. 路径的配置必须为绝对路径，但相对路径也不会报错。比较常用的配置方法如下：<br/>
		    `var path = require('path');`
		    
		 	打包输出：`output:{
        			path:path.resolve(__dirname, 'dist/assets'),
        			filename:'index.js'
    			},`
    	2. 在使用webpack时，需要添加HtmlWebpackPlugin组件：<br/>
            `var HtmlWebpackPlugin = require('html-webpack-plugin');`
	         
	         组件配置:
	         `plugins: [
        			new HtmlWebpackPlugin({
            				template: __dirname + "/src/index.html"//new 一个这个插件的实例，并传入相关的参数
        			})
    			]`
			
--------

# 2017/5/17

#Class关键字
- 用法:通过 class关键字,可以定义类,其实质为一个语法糖.
	+ 语法
	`class Point {
  		constructor(x, y) {
    		this.x = x;
    		this.y = y;
  		}								
  		toString() {
    		return '(' + this.x + ', ' + this.y + ')';
  		}
	 }`  
	 + 定义类的方法时不需要加 function 关键词,方法之间无需逗号分隔.其用法和 java基本相似.	 
	 + 在类的实例上调用方法,就是在调用原型上的方法.
	 + 类内部定义的所有方法都是不可枚举的.
	 + 类的属性名可以是表达式.如下:
	 	`let methodName = "getArea";
	  	 class Square{
		 	constructor(length) {
    				// ...
  			}
  			[methodName]() {
    				// ...
  			}
		}`
	<br/>
  	+ constructor方法是类的默认方法,返回值为一个实例对象.实例对象的属性除非显式定义在对象的本身上,否则都定义在原型上.
  	+ 类的所有实例共享一个原型对象.可以通过原型对象的实例__prototype__属性为 class添加方法.
  	+ class不存在变量的提升.
  	+ class中this的指向类的实例.所以推荐使用箭头函数来绑定 this,使其指向外部作用域的 this.
  	+  **注意区分 es5和 es6的继承机制.**两种机制相反.ES5的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）;ES6的继承机制完全不同，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
  	+ 子类继承父类时,子类首先在 constructor中调用 super()方法之后才能使用 this. 子类的构造函数必须执行一次 super 函数.	
  	+ 子类的__proto__属性表示构造函数的继承,总是指向父类.
  		子类的 prototype 属性的__proto__属性表示方法的继承,总是指向父类的 prototype 属性.
  	+ super的两种用法:
  		1.super作为函数调用时，代表父类的构造函数.
  		2.super作为对象,在类的普通方法中指向父类的原型对象;在静态方法中指向父类.(**因为 super指向父类的原型对象,所以定义在父类实例上的方法或属性无法通过 super 获取**).通过 super调用父类的方法时, super会绑定子类的 this. 

--------
# 2017/5/18
##React-Router
- Router是 React的一个组件.Router组件本身只是一个容器,路由要通过 Route组件定义.
	+ 参数 history,值为 hashHistoy.表示路由切换由URL的 hash变化决定.
	+ 可以使用多个 Route组件来定义 URL和组件的映射关系.
	
##嵌套路由
- 可以在 Route组件中嵌套多层 Route 组件来形成嵌套加载关系,按照嵌套次序依次加载组件.
	+ Link 组件是`<a>`标签的 React 版本,可以接收 Router的状态.
	
## IndexRoute组件
- 该组件是为了显式的指定默认情况下加载的子组件.可以理解为某个路径下的 index.html.

## Redirect组件
- 该组件用于路由的跳转,用户访问一个路由,会自动跳转到另一个路由.
	+ 语法:
	
	`<Route path="inbox" component={Inbox}>
  		{/* 从 /inbox/messages/:id 跳转到 /messages/:id */}
  		＜Redirect from="messages/:id" to="/messages/:id" />
	</Route>`
		
## IndexRedirect组件
- 语法:
		`<Route path="/" component={App}>
  			＜IndexRedirect to="/welcome" />
  			<Route path="welcome" component={Welcome} />
  			<Route path="about" component={About} />
		</Route>`
- 用户访问根路径时,将重定向到子组件 welcome.
