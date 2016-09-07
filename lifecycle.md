### 组件的生命周期 
一个组件就是一个状态机：对特定的输入，总会返回一致的输出。

在组件的整个生命周期中，随着组件的props或者state发生改变，它的DOM表现也将有相应的变化。React为每个组件提供了生命周期钩子函数去响应不同的时刻：创建时、存在期、销毁时。

###### 生命周期方法

React组件拥有简洁的生命周期API，仅提供需要的方法，不追求全面。

1.1 实例化

初次创建一个实例，调用的生命周期方法和后续实例创建调用的方法不同。首次使用一个组件类时，依次调用：

> getDefaultProps

（只被调用一次。为初次创建的实例设置默认的props值）

值得注意的是，任何复杂的值，比如对象和数组，都会在所有的实例中共享，而不是拷贝或克隆。

> getInitialState

（每次实例创建时调用一次。在这里初始化实例的state）

在这个方法里，已经可以访问到this.props。

componentWillMount（在完成首次渲染之前调用）

也是在render方法调用前可以修改组件state的最后一次机会。

render（创建一个虚拟DOM，用来表示组件到输出）

只能通过this.props和this.state访问数据。

可以返回null、false或者任何React组件。

只能出现一个顶级组件（不能返回一组元素）。

必须纯净，意味着不能改变组件的状态或者修改DOM的输出。

componentDidMount（真实的DOM<内存中的DOM表现>已经被渲染之后，在componentDidMount内部通过this.getDOMNode()方法访问到它）

1.2 存在期

依次调用：

componentWillReceiveProps

shouldComponentUpdate

componentWillUpdate

render

componentDidUpdate

1.3 销毁清理期

调用：componentWillUnmount，给实例提供清理自身的机会。
