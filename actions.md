### Action 

> 组件中使用 this.$store.dispatch('xxx') 分发 action，

> 或者使用 mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用（需要先在根节点注入 store）

类似于 mutation，不同在于：

1. Action 提交的是 mutation，而不是直接变更状态。

2. Action 可以包含任意异步操作。

```
  actions: {
    increment (context) {
      context.commit('increment')
    }
  }
```
**context 对象** 与 store 实例具有相同方法和属性

context.commit

context.state

context.getters

```
//  参数解构 来简化代码
actions: {
  incrementAsync ({ commit }) {
    setTimeout(() => {
      commit('increment')
    }, 1000)
  }
}
```

#### 分发 Action
Action 通过 store.dispatch 方法触发：
```
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

购物车示例，涉及到调用异步 API 和 分发多重 mutations：

进行一系列的异步操作，并且通过提交 mutation 来记录 action 产生的副作用（即状态变更）
```
actions: {
  checkout ({ commit, state }, products) {
    // 把当前购物车的物品备份起来
    const savedCartItems = [...state.cart.added]
    // 发出结账请求，然后乐观地清空购物车
    commit(types.CHECKOUT_REQUEST)
    // 购物 API 接受一个成功回调和一个失败回调
    shop.buyProducts(
      products,
      // 成功操作
      () => commit(types.CHECKOUT_SUCCESS),
      // 失败操作
      () => commit(types.CHECKOUT_FAILURE, savedCartItems)
    )
  }
}
```

#### 组合 Actions
store.dispatch 可以处理被触发的action的回调函数返回的Promise，并且store.dispatch仍旧返回Promise：
```
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
```
现在你可以：
```
store.dispatch('actionA').then(() => {
  // ...
})
```
在另外一个 action 中也可以：
```
actions: {
  // ...
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
      commit('someOtherMutation')
    })
  }
}
```
最后，如果我们利用 async / await 这个 JavaScript 即将到来的新特性，我们可以像这样组合 action：

```
// 假设 getData() 和 getOtherData() 返回的是 Promise

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
```
>一个 store.dispatch 在不同模块中可以触发多个 action 函数。在这种情况下，只有当所有触发函数完成后，返回的 Promise 才会执行。