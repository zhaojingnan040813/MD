
### 1. 说说对 React 的理解? 有哪些特性?        


### 2. state 和 props 有什么区别? 

```md
props
理解为从外部传入组件内部的数据  
一个组件的显示形态可以由数据状态和外部参数所决定，而数据状态就是state，一般在constru
ctor 中初始化
当需要修改里面的值的状态需要通过调用setstate 来改变，从而达到更新组件内部数据的作用，

相同点：
• 两者都是 JavaScript 对象
• 两者都是用于保存信息
• props 和 state 都能触发渲染更新

区别：
• props 是外部传递给组件的，而 state 是在组件内被组件自己管理的，一般在 constructor 中初始化
• props 在组件内部是不可修改的，但 state 在组件内部可以进行修改
• state 是多变的、可以修改

```
### 3. super()和 super(props) 有什么区别?
```
必须先初始化 super() 然后才能调用 this      

在类组件当中，在调用 super() 的时候，即使你不传 props 进去，React 内部也会讲 props 注入到组件实例里面，但是也不建议使用super()代替super(props)  --> 原因略

如果只调用了 super()，那么 this.props 在 super()和构造函数结束之间仍是 undefined

```

### 4. 说说对React中类组件和函数组件的理解?有什么区别?（必会）
```
有点像 Vue2 与 Vue3的发展 （在我的项目当中用的都是函数式组件）
从编写形式，生命周期，调用方式 这些方面来回答。
```

### 5. 说说对受控组件和非受控组件的理解?应用场景?
```MarkDown
受控组件一般需要一个状态更新事件函数，

| **维度**         | **受控组件**                          | **非受控组件**                      |
|------------------|--------------------------------------|-------------------------------------|
| **数据源**       | React 的 `state`                     | DOM 节点的 `value` 属性              |
| **更新方式**     | 通过 `onChange` 事件主动更新 `state` | 通过 `ref` 直接读取或修改 DOM 值     |
| **控制权**       | React 完全控制                       | DOM 自主控制                        |
| **代码复杂度**   | 较高（需维护 `state` 和事件处理）    | 较低（依赖 `ref` 即可）             |


```
### 6. 说说React的事件机制 ?
```

```

### 7. React事件绑定的方式有哪些?区别? 

```js
class ShowAlert extends React.Component {
  showAlert() {
    console.log(this);
  }

  render() {
    // return <button onClick={() => this.showAlert()}>show</button>;
    // return <button onClick={this.showAlert.bind(this)}>show</button>;
    // return <button onClick={e=>this.showClick(e)}>show</button>
    return <button onClick={showAlert()}>show</button>;
  }
}
问：打印结果为什么是 underfine 如何解决？

* render 方法中使用bind
* render 方法中使用箭头函数
* constructor中bind
constructor(props) {
  super(props);
  this.handleClick = this.handleClick.bind(this);
}
​​super(props)​​：调用父类 React.Component 的构造函数，确保 this 指向当前组件实例例。       
​​bind(this)​​：将 handleClick 方法的 this 强制绑定到组件实例，避免事件触发时 this 丢失上下文。

* 定义阶段使用箭头绑定(最推荐)
showAlert=()=>{console.log(this)}
```

### 8. React构建组件的方式有哪些?区别?
```md
1. 函数式创建 (React.Hooks，推荐)
2. 通过React.creatClass 方法创建 (基本已经不用了,但是它是babel的最终转化形式)
3. 继承React.Component 创建 
```

### 9.说说react中引入css的方式有哪几种?区别?
```

```
### 10 .说说 React 生命周期有哪些不同阶段？以及每个阶段对应的方法
```
比Vue难背，
挂载阶段: constructor , render , componentDidMount 
更新阶段： render, shouldComponentUpdate, componentDidUpdate
卸载阶段：component-Will-Unmount

 ​新项目优先使用函数组件（useEffect ） + Hooks​​，避免类组件的复杂性。

```

### 11. React中组件之间如何通信?
```md
1. 父传子 --------> 子组件中定义props属性
2. 子传父 ---> 父组件向子组件传一个函数，然后通过这个函数的回调，拿到子组件传过来的值
3. 兄弟组件通信
4. 多级组件传递
5. 非关系组件传递

```

