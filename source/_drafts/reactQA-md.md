---
title: React QA
tags:
- job
---

### 类组件和函数组件的区别是什么？
```
特性        类组件              函数组件

语法        ES6 class           普通函数
状态        有 (this.state)     使用 useState
生命周期    有                  使用 useEffect
this        需要绑定            不需要
性能        稍慢                更快
Hooks       不能使用            可以使用
```

### React 中的状态提升是什么？
- 状态提升是将多个组件需要共享的状态移动到它们最近的共同父组件中的过程。这样做可以：
- 保持组件间数据同步
- 实现"单一数据源"原则
- 使组件更可预测和可维护
- 示例：多个输入框需要同步数据时，将状态放在它们的父组件中。

### 解释 React 的生命周期方法
类组件的主要生命周期方法：

- 挂载阶段：
    - constructor()：初始化状态和绑定方法
    - static getDerivedStateFromProps()：在 render 前调用
    - render()：渲染组件
    - componentDidMount()：组件挂载后调用，适合副作用操作

- 更新阶段：
    - componentDidUpdate()：更新后调用

- 卸载阶段：
    - componentWillUnmount()：清理工作

### 解释 React Hooks 及其优势
- Hooks 是 React 16.8 引入的特性，允许在函数组件中使用状态和其他 React 特性。
- 主要 Hooks：
    - useState：管理状态
    - useEffect：副作用操作
    - useContext：访问上下文
    - useReducer：复杂状态逻辑
    - useCallback：记忆函数
    - useMemo：记忆值
    - useRef：访问 DOM 或保持可变值

- 优势：
    - 简化组件逻辑
    - 复用状态逻辑而不改变组件层次
    - 更易于理解和测试的代码
    - 减少类组件中 this 的困惑

### useEffect 与 useLayoutEffect 的区别？
- 一般优先使用 useEffect，只有在需要 同步测量 或 操作 DOM 时才使用 useLayoutEffect。

### 如何优化 React 应用性能？
- 使用 useCallback/useMemo：记忆函数和值，避免重新创建
- 代码分割：使用 React.lazy 和 Suspense 进行 lazy load
- 避免内联函数和对象：作为 props 传递时会导致子组件不必要更新
- 使用 key 属性：帮助 React 识别元素变化
- 分析工具：使用 React DevTools Profiler 识别性能瓶

### 什么是 React 的 reconciliation 算法？
- Reconciliation 是 React 更新 DOM 的过程，通过比较新旧虚拟 DOM 树来确定最高效的更新方式。

- Diffing 算法原则：
    - 不同类型元素：完全重建子树
    - 相同类型 DOM 元素：仅更新改变的属性
    - 相同类型组件元素：保持实例，更新 props
    - 列表比较：使用 key 属性识别元素是否移动/改变

优化点：为列表项提供稳定、唯一的 key，避免使用索引作为 key（除非列表不会重新排序）。

###  如何在 React 中处理异步操作？
处理异步操作的常见方法：

#### useEffect + 状态：
```js
useEffect(() => {
  let isMounted = true;
  const fetchData = async () => {
    try {
      const result = await apiCall();
      if (isMounted) setData(result);
    } catch (error) {
      if (isMounted) setError(error);
    }
  };
  
  fetchData();
  
  return () => { isMounted = false; };
}, [dependencies]);
```

#### Redux Saga
Generator 函数在 Redux Saga 中的作用
- Generator 函数（使用 function* 语法）是 Redux Saga 的核心，它：
- 通过 yield 返回 Effect 对象（简单的 JavaScript 对象），这些对象包含中间件执行的指令
```js
function* fetchUser() {
  // 暂停直到 call 完成
  const user = yield call(api.fetchUser);
  // 暂停直到 put 完成
  yield put({type: 'FETCH_USER_SUCCESS', user});
}
```

什么是 Effect？列举常见的 Effect creators
- call(fn, ...args)：调用函数（通常是异步函数）
- put(action)：dispatch 一个 action
- take(pattern)：等待指定的 action
- race([...effects])：运行多个 Effects，取第一个完成的结果
- select(selector, ...args)：获取 store 中的 state
- takeEvery(pattern, saga)：每次 action 匹配时派生一个 saga
- takeLatest(pattern, saga)：只执行最新的 saga（取消之前的）

```js
// 处理 API 请求
import { call, put, takeEvery } from 'redux-saga/effects';
import api from './api';

// worker Saga
function* fetchUser(action) {
  try {
    const user = yield call(api.fetchUser, action.payload.userId);
    yield put({type: 'FETCH_USER_SUCCESS', user});
  } catch (error) {
    yield put({type: 'FETCH_USER_FAILURE', error});
  }
}

// watcher Saga
function* watchFetchUser() {
  yield takeEvery('FETCH_USER_REQUEST', fetchUser);
}

// 或者使用 takeLatest 避免重复请求
function* watchFetchUser() {
  yield takeLatest('FETCH_USER_REQUEST', fetchUser);
}
```

```js
// 轮询（polling）
import { call, put, delay } from 'redux-saga/effects';
import api from './api';

function* pollData() {
  while (true) {
    try {
      const data = yield call(api.fetchData);
      yield put({type: 'DATA_FETCH_SUCCESS', data});
      yield delay(5000); // 等待5秒
    } catch (error) {
      yield put({type: 'DATA_FETCH_FAILURE', error});
      yield delay(5000); // 出错也等待5秒再重试
    }
  }
}

// 可以添加取消逻辑
function* watchPollData() {
  const task = yield fork(pollData);
  yield take('STOP_POLLING');
  yield cancel(task);
}
```

```js
// 测试 Redux Saga
import { call, put } from 'redux-saga/effects';
import { fetchUser } from './sagas';
import api from './api';

test('fetchUser Saga test', () => {
  const generator = fetchUser({payload: {userId: 1}});
  
  // 测试第一个 yield (call effect)
  expect(generator.next().value).toEqual(call(api.fetchUser, 1));
  
  // 模拟成功响应
  const mockUser = {id: 1, name: 'John'};
  expect(generator.next(mockUser).value).toEqual(
    put({type: 'FETCH_USER_SUCCESS', user: mockUser})
  );
  
  // 测试是否结束
  expect(generator.next().done).toBe(true);
  
  // 也可以测试错误情况
  const errorGenerator = fetchUser({payload: {userId: 1}});
  errorGenerator.next();
  expect(errorGenerator.throw('error').value).toEqual(
    put({type: 'FETCH_USER_FAILURE', error: 'error'})
  );
});
```
  
```js
// 使用 all Effect 来实现并行任务
import { all, call } from 'redux-saga/effects';

function* fetchAll() {
  // 并行执行，等待所有完成
  const [users, posts] = yield all([
    call(fetchUsers),
    call(fetchPosts)
  ]);
  
  // 或者使用 race 只取第一个完成的结果
  const { posts, timeout } = yield race({
    posts: call(fetchPosts),
    timeout: call(delay, 1000)
  });
}
```




