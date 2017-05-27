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
## React-Router
- Router是 React的一个组件.Router组件本身只是一个容器,路由要通过 Route组件定义.
	+ 参数 history,值为 hashHistoy.表示路由切换由URL的 hash变化决定.
	+ 可以使用多个 Route组件来定义 URL和组件的映射关系.
	
## 嵌套路由
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

## antD-table组件
- 可以使用 rowSelection属性来让表格中每行都可被选中.其值为一个对象,该对象中包含事件监听.如下:
	+
	`const rowSelection = {
  		onChange: (selectedRowKeys, selectedRows) => {
    		console.log('selectedRowKeys: ${selectedRowKeys}, 'selectedRows: ', 			selectedRows);
  	},
  	getCheckboxProps: record => ({
    	disabled: record.name === 'Disabled User',    // Column configuration not to be 												      checked
  	}),
	};`
	
---------	
	
# 2017/5/19

1. IndexLink组件
	- 作用:需要链接到根路由,防止根路由的 activeStyle 和 activeClassName 属性失效.要使用IndexLink组件才能进行路径的精确匹配,只有路径精确匹配的情况下,根路由才具有 activeClassName属性和 activeStyle属性.
	- 注:使用Link组件的 onlyActiveOnIndex属性也能在根路由上进行精确匹配.
2. history 属性
	- 值: 
		+ hashHistory:路由通过 URL 的 hash部分(#)切换.
		+ browserHistory:路由通过 History API 完成切换.
		+ createMemoryHistory: 它创建一个内存中的history对象，不与浏览器URL互动.
3. 表单处理
	- 作用: 用于表单跳转,点击按钮跳转式和 Router 对接.
	- 方法:
		+ 使用 browserHistory.push(path). 用获取到的表单数据构建path.
		+ 使用 context对象:`this.context.router.push(path)`
4. 路径通配符
	- 规则:
		+ **:paramName** 该规则匹配 URL的一个部分,直到下一个/,?,#为止.可以通过 this.props.params.paramName 取出.
		+ ():表示 URL这个部分可选.
		+ *:模式匹配
		+ **:匹配任意字符.
				
-----------

# 2017/5/22

## react state
- 可以无需使用 getInitialState 方法,直接在模块内初始化一个 state对象,并为 state 对象设置多个属性,以便以后使用 setState()方法来修改 state.

## 编程风格
- es6中一些编程规则
	+ 静态字符串使用单引号;动态字符串使用反引号;
	+ 使用数组成员对变量进行赋值时,优先使用数组的解构赋值.如下:
	
		`const arr = [1, 2, 3, 4];
		 const [first, second] = arr;`
	+ 如果函数返回多个值,优先使用对象的解构赋值
		`function processInput(input) {
  			return { left, right, top, bottom };
		}`
	+ 对象尽肯能的静态化,一旦定义,尽量避免添加新的属性.如果非要添加,使用Object.assign方法;
		`const a = {};
		Object.assign(a, { x: 3 });
		`
	+ 扩展运算符(...)可以用来拷贝数组:
		<code>
			const itemsCopy = [...items];//将 items的每个元素赋值给 itemCopy的每一个元素
		</code>
		+ 扩展运算符可以将一个数组变为参数序列,结合正常参数非常灵活:
			```
			function f(v, w, x, y, z) { };
			var args = [0, 1];  
			f(-1, ...args, 2, ...[3]);
			```
		+ 扩展运算符可以将数组转为函数的参数,进而直接传递给函数.
			````
			var args = [0, 1, 2];  
			f(...args);  
			```
		+ 扩展运算符和解构赋值配合用于生成数组:`const [first, ...rest] = [1, 2, 3, 4, 5];`.注:扩展运算符用作数组赋值时,只能放在参数的最后一位.
		+ 可以将字符串用扩展运算符转化我数组.	

	+ 立即执行函数和需要使用函数表达式的场合中,尽可能使用箭头函数,而且还绑定了 this;
	+ 使用默认值语法来设置函数参数的默认值:
		`function handleThings(opts = {}) {
  			// ...
		}`
	+ 用import来替代 require;用 export 代替 module.exports.

------------

# 2017/05/23

## react-component的特性
- 纯净函数和非纯净函数
	+ 纯净函数:不改变函数的输入值(如参数等),并且总是给相同的输入返回相同的输出.如下:
		```
		function sum(a, b) {
  			return a + b;
		}
		```
	+ 非纯净函数:和纯净函数相反,非纯净函数将改变自身的输入.如下:
		```
		function withdraw(account, amount) {
  			account.total -= amount;
		}
		```	
	+ 所有的 react-component 都必须像纯净函数一样.
- setState()方法可以接受一个函数作为参数.该函数的第一个参数是上一个状态,第二个参数是应用更新时的props.如下:
	```
	this.setState((prevState, props) => ({
  		counter: prevState.counter + props.increment //返回 state对象
	}));
	```
- react 承接事件时不能使用 `return false` 来阻止默认行为,要使用 preventDefault()方法.
	+ 一般情况下,使用 react 无需给 DOM 元素分配事件,而是直接给元素一个监听器.
	
------------
# 2017/5/24

## ant-d中table组件
- 在父组件中实现的方法可以放入 props, 然后传递给子组件,在子组件中通过 `this.props.functionName()`进行调用即可.
	+ 父组件中可以定义state并定义改变 state的方法.然后将改变 state的方法传递给子组件,在子组件中进行调用便可以实现子组件改变父组件状态.
	+ 以上的方法实现了父组件和子组件之间的通讯,但该方法非常繁琐.可以考虑到使用 redux.
	
## js遍历对象属性的常见方法
- js中几种遍历对象的方法，包括for in、Object.keysObject.getOwnProperty,它们在使用场景方面各有不同。
	+ for in主要用于遍历对象的可枚举属性，包括自有属性、**继承自原型的属性**.如下：
		```
		var obj = {"name":"Poly", "career":"it"}
		Object.defineProperty(obj, "age", {value:"forever 18", enumerable:false});
		Object.prototype.protoPer1 = function(){console.log("proto");};
		Object.prototype.protoPer2 = 2;
		console.log("For In : ");
		for(var a in obj) console.log(a);// name career protoPer1 protoPer2
		```
	+ Object.keys.返回一个数组，数组元素均为对象自有的**可枚举**属性.
		```
		var obj = {"name":"Poly", "career":"it"}
		Object.defineProperty(obj, "age", {value:"forever 18", enumerable:false});
		Object.prototype.protoPer1 = function(){console.log("proto");};
		Object.prototype.protoPer2 = 2;
		console.log("Object.keys:")
		console.log(Object.keys(obj)); //["name",'career']
		```
	+ Object.getOwnProperty,返回对象的自身的**全部属性**。
		```
		var obj = {"name":"Poly", "career":"it"}
		Object.defineProperty(obj, "age", {value:"forever 18", enumerable:false});
		Object.prototype.protoPer1 = function(){console.log("proto");};
		Object.prototype.protoPer2 = 2;
		console.log("Object.getOwnPropertyNames: ");
		console.log(Object.getOwnPropertyNames(obj));//["name","career","age"]
		```
---------
# 2017/05/25
## react list key
- 作用:唯一的标识列表项,最好为通过 map()方法生成的列表项添加key,而不是直接添加到`<li>`元素上.如下:
	```
	const listItems = numbers.map((number) =>
       <ListItem key={number.toString()} value={number} />
  	);
	```
- 如果需要在组件中获取和key值相同的值，**不能使用this.props.key**,而要使用this.props.anotherName。

# 2017/05/26
## redux设计思路
- view与state一一对应;所有的state 保存在 store 里.state的变化是由view 导致的,view发出的Action便可以让 store 接收.	
	- store
		+ store的生成: `const store=createStore(fn);`
	- state包含某个时点的 `state=store.getState();`
	- action是改变 state 的唯一办法,使用 action就可以运送数据到 store.
		```
		const action = {
  			type: 'ADD_TODO',
  			payload: 'Learn Redux'
		};
		```
	- `store.dispatch(actionObj)`是 view 发出 Action的唯一方法:参数为一个 action对象.
- reducer:store 收到 action 之后,给出新的 state之后就会导致 view的变化,state 的计算过程为 reducer.
	+ reducer一般不会手动调用,在创建 store的时候直接将reducer 传递给 createStore(reducer)方法.
	+ 
	 
## react-state的共享问题
- 场景:当多个组件需要同步state的时候,就可以将state提升到这些组件共有的父组件中.在父组件中通过 props来配置.
- 如果在一个父组件中并不知道将来会为其添加多少子组件,那么可以在父组件中加入`this.props.children`,利用该属性,在将来为父组件内添加内容时,以前定义的父组件中自动会加入所有的内容.这个属性可以用在模板代码块上,在用该模板来实现组件时改写模板即可.
-----------
# 2017/05/27
## redux学习笔记_2
- **redux 工作流程**:
	1. 用户发出 action,`store.dispatch(action)`.
	2. store 自动调用 reducer,并传入参数:当前 state和收到的 action.之后 reducer返回新的 state.
	`let nextState=todo(previousState,action);`
	3. state 发生变化, store 调用监听函数.
	`store.subcribe(listener)`
	4. 监听函数 listener 可以通过 `store.getState()`得到当前的状态.进而出发重新渲染 View.
- store的实现:
	+ 方法: store.getState(),store.dispatch(),store.subcribe()
	+ createStore(reducer,window.State_from_server),第二个参数为服务器给出的初始状态,有此参数就会覆盖 reducer初始值.
## babel class-transform
- 在 class 中写箭头函数报语法错误,后来发现是因为 babel class转化的问题.是因为不能解析当前的提案语法二导致的.需要安装`"babel-plugin-transform-es2015-classes"`才能解决.
	
