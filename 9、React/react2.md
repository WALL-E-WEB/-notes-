# jsx

```jsx
import React,{Component} from 'react';
import ReactDOM from 'react-dom'

function Root(){
	return <div>
	
        </div>
}

ReactDOM.render( <Root/>,document.getElementById('root') )
```

组件创建方式

无状态组件

```js
function Root(){
	return <div>
	
        </div>
}
export default Root
```

状态组件

```js
import React,{Component} from 'react';
class Root extends Component{
    render(){
        return <div> <div/>
    }
}
export default Root
```

![1581764358114](D:\CODE-Item\-notes-\9、React\react2.assets\1581764358114.png)

# react生命周期

 ![img](D:\CODE-Item\-notes-\9、React\react2.assets\10306662-b1113e690ef13a8d.webp) 

![çå½å¨æç¤ºæå¾](D:\CODE-Item\-notes-\9、React\react2.assets\component_life.jpg)

![1581764766584](D:\CODE-Item\-notes-\9、React\react2.assets\1581764766584.png)

### 初始挂载

```
constructor

componentWillMount(){}

render(){}

componentDidMount(){}


```

### 更新阶段

```js
componentWillReceiveProps（newProps  ）{}
//componentWillReceiveProps在初始化render的时候不会执行，它会在Component接受到新的状态(Props)时被触发，一般用于父组件状态更新时子组件的重新渲染。

shouldComponentUpdate(){}
//返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。

componentWillUpdate(nextProps, nextState){} 
//在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。

render(){}

componentDidUpdate(prevProps, prevState){}
//在组件完成更新后立即调用。在初始化时不会被调用
```

	>componentWillReceiveProps
	>
	>```js
	>// 这种方式十分适合父子组件的互动，通常是父组件需要通过某些状态控制子组件渲染亦或销毁...
	>
	>componentWillReceiveProps(nextProps) {//componentWillReceiveProps方法中第一个参数代表即将传入的新的Props
	>    if (this.props.sharecard_show !== nextProps.sharecard_show){
	>        //在这里我们仍可以通过this.props来获取旧的外部状态
	>        //通过新旧状态的对比，来决定是否进行其他方法
	>        if (nextProps.sharecard_show){
	>            this.handler();
	>        }
	>    }
	>}
	>```
	>
	>shouldComponentUpdate
	>
	>```js
	>shouldComponentUpdate(nextProps,nextState){
	>	return true   //为true则往下执行render
	>}
	>```
	>
	>

### 销毁

```js
componentWillUnmount(){}
```

### 案例

```js
class Root extends Component{
	constructor(props){
		super(props)
        this.state
	}
	componentWillMount(){
        //无法获取dom
        //render修改state的最后阶段
    }
	render(){}
	componentDidMount(){
        //获取Dom
        //1.定时任务
        //2.插件的实例化
        //3.网络请求
        //4.事件监听
        this.setState(){}
    }
    
    componentWillReceiveProps（nextProps）{}
}
```

# 数据类型

![1581767553087](D:\CODE-Item\-notes-\9、React\react2.assets\1581767553087.png)

```

```

# css样式书写

![1581767676626](D:\CODE-Item\-notes-\9、React\react2.assets\1581767676626.png)

### 1.行内样式

```js
const style={
	p:{
		color：'red'
	}
}

class Root extends Component{
	render(){
		return <div style={style.p}> </div>
	}
}
```

## 2.全局样式

​	html引入

```js
index.html
<link rel="stylesheet" href="/base.css">
```

​	importy引入

```js
import './css/base.css'
```

## 3.css-modules

解决css污染

```js
a.module.css //css的文件名

组件中引入
import style from './a.module.css'

class Test extends Component {
    render() {
        return (
            <div>
                <div className={styles.类名}>测试</div>
            </div>
        )
    }
    
https://www.cnblogs.com/crazycode2/p/8593143.html
```

# react事件处理

![1581769752060](D:\CODE-Item\-notes-\9、React\react2.assets\1581769752060.png)

```js
react把事件代理到顶级节点
```

## this的绑定

### 1.constructor-bind

```jsx
class Root extends Component{
	constructor(props){
		super(props)
		this.change=this.change.bind(this)
	}
    change（）{
    	console.log('s')
    }
    render(){
        return <div>
        	<button onClick={this.change}>按钮</button>
        </div>
    }
    
}
```

### 2.dom中（）=>

```jsx
 render(){
        return <div>
        	<button onClick={()=>this.change()}>按钮</button>
        </div>
    }
```

### 3.定义函数

```js
change=（）=>{
	console.log('s')
}
```

# 条件判断

|| && ?

```jsx
class Root extends Component{
    state={
        name:false
        age:true
    }
	render(){
        return <div>
        	{this.state.name || this.state.age}
            {this.state.name && this.state.age}
            {this.state.name? 'a':'b'}
        </div>
    }
}
```

## if

```jsx
class Root extends Component{
    state={
        name:false
        age:true
    }
	render(){
        if(age){
           
        }
        return <div>
        </div>
    }
}
```

```js
 if(props.isLogin==true){
        return <h2>欢迎回来！</h2>
    }else{
        return <h2>请登录！</h2> 
    }
```

```jsx
function Login(props){
    return <h2>欢迎回来！</h2>
}
function Logout(props){
    return <h2>请登录！</h2>
}
function Loginstate2(props){
    if(props.isLogin==true){
        return <Login />
    }else{
        return <Logout />
    }
}
ReactDOM.render(<Loginstate2 isLogin={true}/>,document.getElementById('root'));
```

# 列表渲染

```jsx
render(){
    let ren=[]
    for(const item of this.state.arr){
        ren.push(<li key={item.id}>item</li>)
    }
    return <div>
    	<ul>
        	{ren}
        </ul>
    </div>
}
```

```jsx
render(){
    let ren=[]
    for(const item of this.state.arr){
        ren.push(<li key={item.id}>item</li>)
    }
    return <div>
    	<ul>
        	{
                this.state.arr.map((item.index)=>{
                    return <li key={item}>{item}</li>
                })
            }
        </ul>
    </div>
}
```

