## lesson 10
#### 用浏览器History(API)清理URLs
现在我们app中的url都建立在一个hack上——hash。这是一个默认选项，因为其总是能运行良好，但是这里还有一个更好的解决方案

现代浏览器拥有可以不用发送http请求就能够去修改url的能力，所以我们不必非得依靠url中的hash `#` 部分去分发路由，但是这里有一个坑（我们将在稍后碰到）

配置浏览器的History(API)
打开 `index.js` 导入 `browserHistory` 来代替 `hashHistory` 

```javascript
//index.js
//...
//用browserHistory代替hashHistory
import { Router, Route, browserHistory } from 'react-router'

render((
	<Router history={browserHistory}>
		{/* ... */}
	</Router>
), document.querySelector('#app'));
```

现在开始点击并欣赏下干净的URLs

看吧，一个错误，点击一个链接，并刷新一下浏览器，看看怎么了

`Cannot GET /repos`

#### 配置你的服务

你的服务器需要去运行app无论使用什么url，因为你的app在浏览器中操作url。我们当前的服务器并不知道该怎么处理url。

Webpack Dev Server提供了一个配置可以做到这一点，打开 `package.json` 并增加一行代码 `--history-api-fallback`

```
"start" : "webpack-dev-server --inline --content-base . --history-api-fallback"
```

我们还要把相对路径变成绝对路径在 `index.html` 中，因为URLs将在更深层的路径中，并且如果app在更深层的路径中启动时，他将会因为路径错误无法去找到文件

```
<!-- index.html -->
<!-- index.css -> /index.css -->
<link rel="stylesheet" href="/index.css">

<!-- bundle.js -> /bundle.js -->
<script src="/bundle.js"></script>
```

如果服务运行的话先停止你的服务，然后再次运行 `npm start` ，看看那些干净的URLs吧 :)

