### mutations
Vuex 中的 mutations 非常类似于事件：

每个 mutation 都有

**事件类型 (type)** 一个字符串。

以store.commit 方法调用(type)唤醒一个 mutation handler

**回调函数 (handler)** 像是事件注册。

就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数

**提交载荷（Payload）** store.commit 传入额外的参数，即 mutation 的 载荷（payload）

```
// 对象风格的提交方式
store.commit({
type: 'actionName',
...payload
})
```
**Mutations 需遵守 Vue 的规则**

1. 最好提前在你的 store 中初始化好所有所需属性。

2. 当需要在对象上添加新属性时，你应该

1. 使用 Vue.set(obj, 'newProp', 123), 或者 -

2. 以新对象替换老对象。例如，利用 stage-3 的对象展开运算符我们可以这样写：
```
state.obj = { ...state.obj, newProp: 123 }
```
3. mutation 必须是同步函数
