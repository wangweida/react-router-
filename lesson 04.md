## lesson 04
#### 嵌套路由
我们添加在 **App** 组件中的导航或许应该被添加在每一屏中，如果不通过React Router 我们可以把 **ul** 包装成一个 **Nav** 组件，然后将 **Nav** 组件渲染到每一屏上。
但是这种方法随着app的不断迭代会变得越来越臃肿，所以React Router提供给我们另一种方法————嵌套路由。

#### 嵌套的UI与URLs
你曾经注意到过你写的的app或许很像一层套一层的盒子，并且url往往都是耦合嵌套的吗？举个栗子， **/repos/123** ，我们的组件或许是写成类似下面这种形式的
```
<App> 				{/*      /       */}
	<Repos>				{/*    /repos    */}
		<Repo/>			{/*  /repos/123  */}
	</Repos>
</App>
```

我们的ui像是这样的
```
  		   +-------------------------------------+
         | Home Repos About                    | <- App
         +------+------------------------------+
         |      |                              |
Repos -> | repo |  Repo 1                      |
         |      |                              |
         | repo |  Boxes inside boxes          |
         |      |  inside boxes ...            | <- Repo
         | repo |                              |
         |      |                              |
         | repo |                              |
         |      |                              |
         +------+------------------------------+
```

react-router就采用这种模式，它可以通过你的嵌套路由来自动的生成被嵌套的ui

#### 共享我们的导航
让我们把 **About** 与 **Repos** 这两个Route嵌套进 **App** 的Route中，以便我们可以在app中的所有屏幕上共享导航。
1. 将路径是repos与about的两个route放在app这个route中
```
//index.js
//...

render((
	<Router history={hashHistory}>
		<Route path="/" component={App}>
			<Route path="/about" component={About}/>
			<Route path="/repos" component={Repos}/>
		</Route>
	</Router>
), document.querySelector('#app'));
```

2. 在 **App** 组件内，使用this.props.children渲染子组件
```
//modules/App.js
//...

class App extends React.Component {
	render() {
		return (
			<div>
        		<h1>React Router Tutorial</h1>
        		<ul role="nav">
          		<li><Link to="/about">About</Link></li>
          		<li><Link to="/repos">Repos</Link></li>
        		</ul>
				{this.props.children}
      	</div>
		);
	}
}

export default App;
```

OK，现在去点击链接，**App** 组件将会通过子路由的切换去渲染this.props.children
React Router将会创建你的ui像下面这种形式
```
// at /about
<App>
  <About/>
</App>

// at /repos
<App>
  <Repos/>
</App>
```

#### 量变最终引起质变
构建一个大型项目最好的方式就是将很多小项目组合在一起
这才是React Router真正的力量，每一个子route都可以作为一个独立的应用单独被开发甚至渲染。你的route配置将这些所有app以你喜欢的方式组合在一起，app中包含着app正如盒子中嵌套着盒子

但如果你把 **About** 组件移出 **App** 组件又将会发生什么那？试试看吧！