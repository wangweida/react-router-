## lesson 03
#### 通过Link导航
或许在app中最常用的组件就是 **Link** ，除了只能在Router组件中渲染，它几乎与`<a/>`一模一样
让我们在 **App**组件 中创建几个导航

```
//modules/App.js
import React from 'react.js';
import { Link } from 'react-router';

class App extends React.Component {
	render() {
		return (
			<div>
        		<h1>React Router Tutorial</h1>
        		<ul role="nav">
          		<li><Link to="/about">About</Link></li>
          		<li><Link to="/repos">Repos</Link></li>
        		</ul>
      	</div>
		);
	}
}

export default App;
```

访问[http:localhost:8080] 点击链接，并点击前进后退按钮，简单的单页面应用运行起来了，这实在太牛逼了。