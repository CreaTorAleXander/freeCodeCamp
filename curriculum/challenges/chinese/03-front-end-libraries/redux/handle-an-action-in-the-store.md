---
id: 5a24c314108439a4d4036150
title: 在 Store 里处理 Action
challengeType: 6
forumTopicId: 301444
---

# --description--

在一个 action 被创建并 dispatch 之后，Redux store 需要知道如何响应该操作。这就是`reducer`函数存在的意义。Redux 中的 Reducers 负责响应 action 然后进行状态的修改。`reducer`将`state`和`action`作为参数，并且它总是返回一个新的`state`。我们要知道这是 reducer 的**唯一**的作用。它不应有任何其他的作用：比如它不应调用 API 接口，也不应存在任何潜在的副作用。reducer 只是一个接受状态和动作，然后返回新状态的纯函数。

Redux 的另一个关键原则是`state`是只读的。换句话说，`reducer`函数必须**始终**返回一个新的`state`，并且永远不会直接修改状态。Redux 不强制改变状态，但是你需要在你的 reducer 函数的代码中强制执行它，你将在以后的挑战中练习这一点。

# --instructions--

代码编辑器中具有前面的示例以及一个`reducer`函数。你需要完善`reducer`函数的内容，使得它如果收到类型为`'LOGIN'`的action，它将返回一个将`login`设置为`true`的 state 对象。否则，它就返回当前的`state`。请注意，当前`state`和dispatch的`action`将被传递给reducer，因此你可以使用`action.type`直接获取 action 的类型。

# --hints--

调用`loginAction`函数应该返回一个对象 {type:"LOGIN"}。

```js
assert(loginAction().type === 'LOGIN');
```

store 应该初始化一个对象 {login:false}。

```js
assert(store.getState().login === false);
```

dispatch `loginAction`后应将 store 中 state 的`login`值更新为`true`。

```js
assert(
  (function () {
    const initialState = store.getState();
    store.dispatch(loginAction());
    const afterState = store.getState();
    return initialState.login === false && afterState.login === true;
  })()
);
```

如果 action 的类型不是`LOGIN`，那么 store 应返回当前的 state。

```js
assert(
  (function () {
    store.dispatch({ type: '__TEST__ACTION__' });
    let afterTest = store.getState();
    return typeof afterTest === 'object' && afterTest.hasOwnProperty('login');
  })()
);
```

# --solutions--

