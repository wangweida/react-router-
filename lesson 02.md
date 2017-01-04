## lesson 02 
#### 渲染一个Route
React Router本质上是一个组件，所以我们通过这种方式去渲染一个 **Router**

`render(<Router/>, document.querySelector(‘#app’))`
当然，直到我们去设置一个route以前，这将什么也显示不出来。

打开 `index.js` ，然后

	1. 导入 `Router` ， `Route` ， `hashHistory`
	2. 渲染一个 `Router` 组件来代替 `App` 组件
	
```javascript
import { Router, Route, hashHistory } from ‘react-router’

render((
	<Router history={hashHistory}>
		<Route path=“/“ component={App}>
	</Router>
), document.querySelector(‘#app’));
```

通过 `npm start` 将你的服务运行起来，然后访问[http:localhost:8080]

你的屏幕应该依然显示的是Hello React Router，但是这次url中应该有了额外的结构，因为我们使用了 `hashHistory` ，它使用url中的hash部分来管理路由历史记录。当使用真实的url时，这会产生一些额外的垃圾去shim浏览器的一些行为。我们将在一会使用真实的url去避免这个问题并且丢弃掉这些垃圾，但是在此刻，这显然太牛逼了，因为它无需任何服务端的配置。

#### 增加显示额外的两屏
创建两个新的组件

	* modules/About.js
	* modules/Repos.js

```javascript
//modules/About.js
import React from ‘react’;

class About extends React.Component {
	render() {
		return <div>About</div>
	}
}

export default About
```

```javascript
//modules/Repos.js
import React from ‘react’;

class Repos extend React.Component {
	render() {
		return <div>Repos</div>
	}
}

export default Repos
```

然后把它们放到Router组件中，用 `path` 属性将其连接起来

```javascript
//insert into index.js
import About from ‘./modules/About’;
import Repos from ‘./modules/Repos’;

render((
	<Router>
		<Route path=“/“ component={App}/>
		<Route path=“/about” component={About}/>
		<Route path=“/repos component={Repos}/>
	</Router>
), document.querySelector(‘#app’));
```

访问
[http:localhost:8080/#/about]
[http:localhost:8080/#/repos]
