## lesson 09
#### 主链接
注意到我们的app中并没有返回 `Home` 组件中的导航了么？

让我们来增加这样一个Link `/` 看看会发生点什么

```javascript
//in App.js
//...
<li><NavLink to="/">Home</NavLink></li>
```

现在所有的导航都已经完整了，但是等等，有没有发现一些诡异的事情？`Home` 的Link永远是被点选的状态！就像我们之前学到的，当子route处于被点选状态时，父route必然也是被点选的，不幸的是 `/` 是一切的父route！

对于 `Home` 这个Link，我们希望只有在我们真正处于根路径时才处于被点选状态。有两种方法可以实现。

#### 主链接
让我们使用 `IndexLink` 来代替 `NavLink` 

```javascript
//App.js
import { IndexLink } from 'react-router'
//...
<IndexLink to="/" activeClassName="active">Home</IndexLink>
```

现在好了！只有当我们真正处于根路径时，Link才处于被点选状态，点击左右试试吧

#### onlyActiveOnIndex属性
我们依然可以使用 `Link` 通过 `onlyActiveOnIndex ` 属性 _(IndexLink实际上正式Link使用onlyActiveOnIndex属性的包装)_

```javascript
<li><Link to="/" activeClassName="active" onlyActiveOnIndex={true}>Home</Link></li>
```

这很好，但是我们已经抽象出了导航，他们不必知道 `activeClassName ` 的存在

我们在 `NavLink` 组件中使用了延展操作符 `…` ，它将所有属性传递到了Link中，所以我们可以直接在 `NavLink` 中添加此属性。

```javascript
<li><NavLink to="/" onlyActiveOnIndex={true}></NavLink></li>
```




