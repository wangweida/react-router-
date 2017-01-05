## lesson 12
#### 编程化导航栏
尽管大多数的导航都是以链接的形式，你仍然可能需要一些编程化的导航在你的app中以去响应一些表单提交，按钮点击等事件

让我们在 `Repos` 模块中用编程化导航的方式实现一个小的表单

```javascript
import React from 'react'
import NavLink from './NavLink'

export default React.createClass({

  //增加一个方法
  handleSubmit(event) {
    event.preventDefault()
    const userName = event.target.elements[0].value
    const repo = event.target.elements[1].value
    const path = `/repos/${userName}/${repo}`
    console.log(path)
  },

  render() {
    return (
      <div>
        <h2>Repos</h2>
        <ul>
          <li><NavLink to="/repos/reactjs/react-router">React Router</NavLink></li>
          <li><NavLink to="/repos/facebook/react">React</NavLink></li>
          {/* 此处添加一个表单 */}
          <li>
            <form onSubmit={this.handleSubmit}>
              <input type="text" placeholder="userName"/> / {' '}
              <input type="text" placeholder="repo"/>{' '}
              <button type="submit">Go</button>
            </form>
          </li>
        </ul>
        {this.props.children}
      </div>
    )
  }
})
```

这里有两种方式去实现，其中第一种要比第二种简单一些

第一种方法，我们使用在 `index.js` 中传入 `Router` 的 `browserHistory` 单例，然后将新的url推入到历史记录中

```javascript
// modules/Repos.js
import { browserHistory } from 'react-router'

// ...
  handleSubmit(event) {
    // ...
    const path = `/repos/${userName}/${repo}`
    browserHistory.push(path)
  },
// ...
```

这么做会有一个潜在的问题，如果你在 `index.js` 中使用的是不同的history比如 `hashHistory` 那么这个表单就不会正常工作，但是大部分情况下我们使用的都是 `browserHistory` 所以这是一种可以被我们所接受的方法。如果你实在很介意这点，你可以另外建立一个模块去暴露你想在app中用到的所有的历史记录，或者是...

你也可以使用 `Router` 提供上下文的 `router` ，首先，在组件中访问上下文，然后你就可以用它了

```javascript
export default React.createClass({

  // ask for `router` from context
  contextTypes: {
    router: React.PropTypes.object
  },

  // ...

  handleSubmit(event) {
    // ...
    this.context.router.push(path)
  },

  // ..
})
``` 

这样无论什么history你传入到 `Router` 中，历史记录都能被推入。而由于你使用的是上下文，这将比browserHistory单例测试起来更容易一些