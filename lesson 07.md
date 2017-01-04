## lesson 07
#### 更多的嵌套
注意到当点击 **Repos** 的导航后， **Repos** 的导航列表消失了吗，如果我们希望这个导航列表像全局导航一样一直被保留又该怎么做那？

弄懂以上两个问题再继续向下阅读
…
1. 将 **Repo** Route嵌套进 **Repos** Route中，然后在 **Repos** 组件中渲染`this.props.children`

```
//index.js
//...

<Route path="/repos" component={Repos}>
	<Route path="/repos/:userName/:repoName" component={Repo}></Route>
</Route>
```

```
//Repos.js
//...

<div>
	<h2>Repos</h2>
	<ul>
		<li><Link to="/repos/reactjs/react-router">React Router</Link></li>
		<li><Link to="/repos/facebook/react">React</Link></li>
	</ul>

	{this.props.children}
</div>
```

#### 被点选的Link
让我们把之前的 **NavLink** 组件放到 **Repos** 中使用，这样我们就把 **active** 这个类也加入到了这个组件中
```
//Repos.js
//...
import NavLink from './NavLink'

//...
		<li><NavLink to="/repos/reactjs/react-router">React Router</NavLink></li>
		<li><NavLink to="/repos/facebook/react">React</NavLink></li>
//...
```

注意到全局导航中的链接与 **Repos** 中的导航链接都处于被点选状态了吗？当子route处于被点选状态下，父route理所当然也处于此状态，他们都是绿色的！！！