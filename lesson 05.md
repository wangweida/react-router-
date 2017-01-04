## lesson 05
#### 被点选的链接
**Link** 与 **a** 不同之处就在于 **Link** 可以知道当前的路径是否是active状态的，所以你可以给它设定一些不同的样式

#### 点选链接的样式
看一下怎么在 **Link** 中使用内联样式的，把 **activeStyle** 属性加入你的 **Link** 中
```
//modules/App.js

<li><Link to="/about" activeStyle={{color: 'red'}}>About</Link></li>
<li><Link to="/repos" activeStyle={{color: 'red'}}>Repos</Link></li>
```
现在被点选的链接将会变成红色的

#### activeClassName
也可以通过 **activeClassName** 属性添加类名来代替内联样式
```
//modules/App.js

<li><Link to="/about" activeClassName=“active”>About</Link></li>
<li><Link to="/repos" activeClassName=“active”>Repos</Link></li>
```
接下来添加一个样式表
```
//index.html

<link rel=“stylesheet” href=“index.css” />
```

```
//index.css

.active {
	color: green;
}
```
你需要手动的刷新浏览器，因为webpack不能构建我们的index.html

#### 把Link包装成NavLink组件
在你的网站中大多数的link不需要知道他们是被点选状态的，通常只是主要的导航链接知道就可以了。所以把 **Link** 包装起来是很有帮助的，这样可以让你不用非要记住到底哪里写了 **activeStyle** 和 **activeClassName**

在这里我们使用了延展操作符，**…** ，它将 **props** clone了下来，并且 **activeClassName** 被克隆到了我们所期望的组件上。

创建一个新的模块 **NavLink.js** 
```
//modules/NavLink.js
import React from 'react'
import { Link } from 'react-router'

class NavLink extends React.Component {
	render() {
		return <Link {...this.props} activeClassName="active"/>
	}
}

export default NavLink
```

把 **Link** 改成 **NavLink**
```
//modules/App.js
//...
import NavLink from './NavLink'

<li><NavLink to="/about">About</NavLink></li>
<li><NavLink to="/repos">Repos</NavLink></li>
```

组合组件真是太酷了！