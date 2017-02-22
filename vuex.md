Vuex 采用集中式存储管理应用的状态。

vue.js中的“单向数据流” ==》vuex的状态更新规则
```
状态 渲染 组件 ==> 组件调用 store 中的状态 ==> 仅需在计算属性中返回
组件 分发 事件
事件 提交 转换 ==> 组件的 methods 中提交 mutations
转换 改变 状态 
```
Vuex的store（仓库）存放 状态(state)。

改变状态的唯一途径就是显式地提交(commit) mutations

![](https://vuex.vuejs.org/zh-cn/images/vuex.png)


