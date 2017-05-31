#### 模块 state 局部状态

模块内部的 mutation 和 getter，接收的第一个参数是模块的局部状态

模块内部的 action，context.state 是局部状态，根节点的状态是 context.rootState

模块内部的 getter，根节点状态会作为第三个参数：
```
const moduleA = {
// ...
getters: {
sumWithRootCount (state, getters, rootState) {
return state.count + rootState.count
}
}
}
```