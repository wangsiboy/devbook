### 数据流

在React中，数据的流向是单向的。

从父节点传递到子节点，因而组件只需从父节点获取props渲染即可。

**props是什么**

props就是properties的缩写，使用它把任意类型的数据传递给组件。尽可能把props当作数据源。

通过this.props访问props，但绝对不能通过这种方式修改它。；一个组件绝对不可以自己修改自己的props。

1.1 PropTypes

通过在组件中定义一个配置对象，React提供了一种验证props的方式：

```
var SurveyTableRow = React.createClass({
  propTypes: {
    survey: React.PropTypes.shape({
              id: React.PropTypes.number.isRequired
            }).isRequired,
    onClick: React.PropTypes.func
  },
  //...
});
```

组件初始化时，如果传入的属性和propTypes不匹配，则打印console.warn日志。如果时可选的配置，则可以去掉.isRequired。

1.2 getDefaultProps

为组件添加此函数来设置属性的默认值。不过，这应该只针对那些非必要属性。

不能使用任何特定的实例数据。



1.3 State

组件都可以拥有自己的state，state和props的区别在于前者只存在于组件的内部。只保存最简单的数据，即那些组件正常工作时的必要数据。

state可以用来确认一个元素的视图状态。

永远记得要通过this.steState方法修改。
