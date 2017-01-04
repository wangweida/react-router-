## lesson 06	
#### url参数
思考一下以下url

```
/repos/reactjs/react-router
/repos/facebook/react
```

这些url都可以匹配一个类似这样的路径

```
/repos/:userName/:repoName
```

以 **:** 开头的部分是url的参数，参数的值可以用 `this.props.params[name]` 解析出来

#### 添加一个带参数的Route
让我们看看到底要如何以 `/repos/:userName/:repoName` 这个路径来渲染
首先我们需要在route中渲染一个组件，创建一个新的模块 
`modules/Repo.js`

```javascript
//modules/Repo.js
import React from 'react'

class Repo extends React.Component {
	render() {
		return (
			<div>
				<h2>{this.props.params.repoName}</h2>
			</div>
		);
	}
}

export default Repo;
```

打开 `index.js` ，增加一个新route

```javascript
//...
//import Repo
import Repo from './modules/Repo'

render((
	<Router history={hashHistory}>
		<Route path="/" component={App}>
			<Route path="/about" component={About}/>
			<Route path="/repos" component={Repos}/>
			<Route path="/repos/:userName/:repoName" component={Repo}/>
		<Route>
	</Router>
), document.querySelector('#app'));
```

在 `Repos` 模块中增加新的路由

```javascript
//Repos.js
import { Link } from 'react-router'

class Repos extends React.Component {
	render() {
		return (
			<div>
				<h2>Repos</h2>
				
				<ul>
					<li><Link to="/repos/reactjs/react-router">React Router</Link></li>
					<li><Link to="/repos/facebook/react">React</Link></li>
				<ul>
			</div>
		);
	}
}

export default Repos
```

现在测试一下你的链接吧，注意下path中的参数在组件中变成了属性名。在你的组件中 `repoName` 与 `userName` 都可以是 `this.props.params` 的属性，你或许还应该在你的app中增加一些其它类别的属性，这样无论对你还是对用户都更有好处。