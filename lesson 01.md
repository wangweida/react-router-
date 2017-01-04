## lesson 01
#### 建立一个项目
首先你需要准备好nodejs与包管理器npm
当你完成了准备工作后，打开命令行工具，我们将在那里建立我们的项目

###### 将教程clone下来
```
git clone https://github.com/reactjs/react-router-tutorial
cd react-router-tutorial
cd lessons/01-setting-up
npm install
npm start
```
现在访问[http:localhost:8080]
随意看看代码，理解一下我们是如何使用webpack和npm scripts把这个app运行起来的
你应该在浏览器上看到一个Hello React Router的消息

#### 尝试修改一些内容
打开 **modules/App.js** 并将Hello React Router改成类似Hello的文字，浏览器将会随着你的代码自动刷新页面