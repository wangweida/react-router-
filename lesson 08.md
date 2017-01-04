## lesson 08
#### 主路由
当我们访问 `/` 路径时，显示的仅仅是导航与一个空页面。我们希望当我们访问此路径的时候页面会去渲染一个 `Home` 组件。现在，创建一个 `Home` 组件，让我们来看看如何做到这点。

```javascript
//modules/Home.js

class Home extends React.Component {
	render() {
		return <div>Home</div>
	}
}

export default Home;
```

其中一个选择是如果 `App` 中没有渲染任何组件时，就默认渲染 `Home` 组件

```javascript
//modules/App.js
import Home from './Home'

//...
<div>
	{/* ... */}
	{this.props.children || <Home/>}
</div>
//...
```

这将会运行的很好，但是似乎我们更希望 `Home` 组件也像 `About` 与 `Repos` 组件一样是绑定在一个route上的，因为这么做会有以下几点好处

	1. 一个好的数据抽象是要依赖在匹配路由与其组件上的
	2. 可以触发 `onEnter` 钩子函数
	3. 方便代码分离
	
当然，`App` 组件与 `Home` 组件分离也是一个相当重要的原因，这决定了渲染哪个组件是依赖路由配置的。要时刻记得，我们的目标是将一个个小app放到另一些小app中，而不是直接建造一个庞大冗余的app！

在 `index.js` 在增加一个route

```javascript
//index.js
//新的引入
//引入IndexRoute从react-router中
import { Router, Route, hashHistory, IndexRoute } from 'react-router'
import Homer from './modules/Home'

render((
	<Router history={hashHistory}>
		<Route path="/" component={App}>

			<IndexRoute component={Home}>
			
			<Route path="/repos" component={Repos}>
        	<Route path="/repos/:userName/:repoName" component={Repo}/>
     		<Route path="/about" component={About}/>
		</Route>
	</Router>
), document.querySelector('#app'));
```

现在访问 [http:localhost:8080] ，你将看到 `Home` 组件被渲染

注意 `IndexRoute` 是没有 `path` 属性的，当访问根路径 `/` 或是没有路径被匹配时，它就变成了 `this.props.children` 被渲染到页面上

理解IndexRoute可能需要一些时间，你可以试着理解成当我们访问根路径 `/` 服务器就会去查找 `index.html` ，与其类似React Router做了一样的事情，当访问 `/` 时会去渲染 `IndexRoute` 绑定的组件


