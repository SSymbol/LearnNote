## React基础知识
ReactDOM.render 渲染函数
为渲染函数document.getElementById('root') 获取要插入的容器  

### JSX语法
JavaScript + XML语法（HTML）
遇到<> 就是js解析 遇到{}就是HTML语法解析
```
const react ='React';
ReactDOM.render (<h1>Hello { react }!</h1>,document.getElementById('root'));

```
### 元素渲染

（）：如果存在标签结构，并且标签结构要换行，需要用（）括起来
```
function tick(){
    const element = (
        <div>
            <h1>Hello world!</h1>
            <h2>It is {new Date().toLocaleTimeString()}</h2>
        </div>
    ); \\const es6声明方案 声明后不可更改

    ReactDOM.render(element,document.getElementById('root'));
}
setInterval(tick,1000);\\实时刷新 每间隔一秒刷新一次

```


### 组件
组件的后缀可以使js也可以是jsx，创建jsx有语法提示。

1. 用类的形式创建组件
```
class App extends React.Component{
    //渲染函数
    render(){
        return （
        <h1> hello component </h1>
        ）
    }
}

export default App \\导出 外部引用
```
```
export default class home extends React.Component{
\\可以直接导出一个组件
}
```
2. 用hook的形式创建组件

### porps属性
组件的复用性很重要

porps不可被修改 属于父组件 单向数据流
```
class App extends React.Component{
    render(){
        const nav1 = ["首页","视频","学习"];
        const nav2 = ["web","java","node"];
        return(
            <div>
                <MyNav nav={ nav1 }/>\\分别传入不同的数组
                <MyNav nav={ nav2 }/>
            </div>
        )
    }
}


export default class MyNav extends React.Component{
    render(){
        console.log(this.props.nav);
        return(
            <div>
                {/* jsx语法 遇到大括号按照js语法解析 所以里面是js格式的注释 下同 */}
                <ul>
                    {
                        this.props.nav.map((element,index)=>{
                            return <li key={index}>{ element }</li> 
                            \\key作为索引 必须要加 不加会报错
                        })
                    }
                </ul>
            </div>
        )
    }
}


```

### states
```
export default class StateComponent extends React.Component{
    /**
    *组件中的状态：state
    *以前我们操作页面的元素的变化，都是修改DOM，操作DOM
    *但是有了React优秀的框架，我们不再推荐操作DOM，页面元素的改变使用State进行处理
    */

    constructor（porps）{
        super(porps);
        this.state = { //定义state
            count:10
        }
    }

    increment(){
        //setState去改变state的值
        this.setState({  //state本身是个对象 所以要用花括号放在对象里
            count:this.state.count+=1 //count属于state所以必须以这种方式
        })
    }

    decrement(){
        this.setState({  //state本身是个对象 所以要用花括号放在对象里
            count:this.state.count-=1
        })
    }

    clickHandle = () => {
        console.log(this); //箭头函数，此写法可以不绑定this
    }

    render(){
        return(
            <div>
                <p>{ this.state.count }</p>
                <button onClick={ this.increment.bind(this) }>增加</button>
                <button onClick={ this.decrement.bind(this) }>减少</button>
                <button onClick={ this.clickHandler }>关于this</button>
            </div>
        )
    }
}
```

### React生命周期函数
componentWillMount：在组件渲染之前执行->render->componentDidMount:组件渲染之后执行

if state 发生改变->shouldComponentUpdate:返回true允许改变，false代表不允许改变
if true -> componentWillUpdate在数据改变之前执行（state，props） ->render -> componentDidUpdate 数据修改完成（state，props都会触发这个函数）

if props 发生改变-> componentWillReceiveProps->shouldComponentUpdate同上

unmount-> componentWillunmount:

修改props 涉及到子传父然后回传。
子传父！！！ 父传子！！！很重要！！！

### setState更新是同步还是异步
1. setState会引起视图的重绘
2. 在可控的情况下是异步，在非可控的情况下是同步

### 条件渲染

### 列表渲染
主要问题是key
key代表唯一索引，如果数据索引没有发生变化则ui不会重绘，只有发生变化才重绘，节约渲染资源消耗。

### 表单
1. 受控组件 表单内value的值是通过state来管理的 需要有许多的onchange事件
2. 非受控组件 操作dom
    大多数情况下推荐采用受控组件
    但是表单条目特别多的情况下使用非受控组件
### Refs and DOM
1. 管理焦点，文本选择或媒体播放。
2. 触发强制动画。
3. 集成第三方 DOM 库。

### 状态提升
组件间的数据传递，共同的状态提到父级处理，子父级传递

### 组合 VS 继承
this.props.children

### 箭头函数
```
import React from 'react';
import { Button, Pagination } from 'antd';

function App() {

  function pageChange(page, pageSize){
    console.log(page, pageSize);
  }

  // pageChange=(page, pageSize)=>{
  //   console.log(page, pageSize);
  // } 函数组件不支持箭头函数的写法 ，只有类组件才支持

  

  return (
    <div className="App">
      Hello
      <Pagination showQuickJumper defaultCurrent={1} total={500} onChange={pageChange}></Pagination>
    </div>
  );
}

export default App;

```

### 网络请求 fetch
res Response 响应

### 跨域问题 
开发模式下：
    利用环境解决：react 框架提供
生产模式下：
    jsonp cors iframe postMessage
npm run build -》打包生成生产模式 
