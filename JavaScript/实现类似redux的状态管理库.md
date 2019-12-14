[TOC]

#### 基本实现

- 实现梳理:
  - createStore: 创建一个store来存储监听state
  - reducer: 规定一个处理state的映射方案(纯函数),修改state
- createStore具备的功能
  - subscribe => 订阅
  - getState    => 获取当前状态
  - dispatch    => 接收action => reducer => 修改state

> createStore.js的实现

```javascript
const createStore = (initState, reducer) => {
  let state =  initState;
  const listeners= [];

  // 订阅
  const subscribe = listener => listeners.push(listener);
  const dispatch = action => {
    state = reducer(initState, action.type);
    listeners.forEach(listener => listener());
  };

  const getState = () => {
    return state;
  };

  return {
    subscribe,
    dispatch,
    getState
  }
};
```

> 使用:

```javascript
const state = {
  number: 3
};

const reducer = (state, action) => {
  switch (action) {
    case "one": state.number = 1;break;
    case "two": state.number = 2;break;
    default: console.log("return old");
  }
  return state;
};

const store = createStore(state, reducer);

// 订阅
store.subscribe(() => {
  console.log(store.getState());
});

// 触发
store.dispatch({type: "one"});
store.dispatch({type: "two"});
```

存在的问题: 只能接收一个reducer

-----

#### 处理多个reducer

> 思路: 通过一个函数接收一个reducers数组,返回一个合并后的recuder.

```javascript
const combineReducers = (reducers) => {
  let resultState = {};
  return (state, action) => {
    for(let key in reducers) {
      const reducer = reducers[key];
      resultState = reducer(state, action);
    }
    return resultState;
  };
};
```

> 使用

```javascript
const state = {
  number: {
    count: 1
  },
  color: {
    color: "red"
  }
};
// 合并一波
const store = createStore(state, combineReducers({
  number: numberReducer,
  color: colorReducer
}));

// 订阅
store.subscribe(() => {
  console.log(store.getState());
});

// 触发
store.dispatch({type: "reduce"});
store.dispatch({type: "add"});
store.dispatch({type: "add"});
store.dispatch({type: "blue"});
```

存在的问题: state很庞大,揉在一起

----

#### reducer和state的模块化

将recuder和对应的state独立在一个模块中

> colorReducer.js

```javascript
const state = {
  color: "red"
};

const colorReducer = action => {
  switch (action) {
    case "red": state.color = "red";break;
    case "blue": state.color = "blue";break;
  }
  return state;
};

module.exports = {
  colorReducer
};
```

> numberReducer.js

```javascript
const state = {
  number: {
    count: 1
  }
};

const numberReducer = action => {
  switch (action) {
    case "add": state.number.count += 1;break;
    case "reduce": state.number.count -= 1;break;
  }
  return state;
};

module.exports = {
  numberReducer
};
```

> 改装createStore和combineReducers

- 实现梳理
  - createStore: 初始的state不再通过传参获取
  - combineReducers: 更改合并reducer的方式

> createStore.js

```javascript
const createStore = reducer => {
  let state =  {};
  const listeners= [];

  // 发布订阅
  const subscribe = listener => listeners.push(listener);
  const dispatch = action => {
    state = reducer(action.type);
    listeners.forEach(listener => listener());
  };

  // 无改变返回自身
  dispatch({type: Symbol()});

  const getState = () => {
    return state;
  };

  return {
    subscribe,
    dispatch,
    getState
  }
};
```

dispatch({type: Symbol()}); 这行是关键 通过调用dispatch传入Symbol类型获取到对应state作为初始的state

> combineReducers.js: 返回更改的state 如果此次没有改动 则返回合并的state

```javascript
const combineReducers = reducers => {
  return action => {
    let resultState = {};
    for(let key in reducers) {
      const reducer = reducers[key];
      // 记录上次的state
      const lastState = JSON.parse(JSON.stringify(reducer({ type: Symbol() })));
      const nextState = reducer(action);

      if (JSON.stringify(lastState) !== JSON.stringify(nextState)) {
        resultState = nextState;
      }
    }
    if (JSON.stringify(resultState) === "{}") {
      for(let key in reducers) {
        const reducer = reducers[key];
        resultState = {...resultState, ...reducer({ type: Symbol() })}
      }
    }
    return resultState;
  };
};
```

> 使用

```javascript
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}));
```

存在的问题: 如何追溯更改state的原因

------

#### 中间件的开发 =>日志系统

下手方向: dispatch (能够拿到触发的原因type)

> 装饰dispatch方法

```javascript
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}));
const _dispatch = store.dispatch;
// 拓展dispatch
store.dispatch = action => {
  try {
    console.log('action', action);
    _dispatch(action);
  } catch (err) {
    console.error('error: ', err)
  }
};
```

存在的问题: 功能固定、可拓展性差

----

#### 多日志支持

提供一个接口,支持自定义不同功能的中间件

```javascript
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}));

const _dispatch = store.dispatch;
// 自行定义
const logMiddleware = action => {
  console.log('action', action);
};
// 中间件处理
const exceptionMiddleware = (...middleware) => dispatch => action => {
  try {
    middleware.forEach(_middleware => {
      _middleware(action);
    });
    dispatch(action);
  } catch (err) {
    console.error('error: ', err)
  }
};
// dispatch
store.dispatch = exceptionMiddleware(logMiddleware)(_dispatch);

// 订阅
store.subscribe(() => {
  console.log("state", store.getState());
});

// 触发
store.dispatch({type: "reduce"});
store.dispatch({type: "add"});
store.dispatch({type: "add"});
store.dispatch({type: "blue"});
```

------

#### 中间件模块化

开放store,增加中间件可能的功能支持

> exceptionMiddleware.js module

```javascript
const logMiddleware = (store, action) => {
  console.log('action', action);
  console.log('last state', store.getState());
};

const timeMiddleware  = (store, action) => {
  console.log('time', Date.now());
  console.log('last state', store.getState());
};

const exceptionMiddleware = (...middleware) => (store, dispatch) => action => {
  try {
    middleware.forEach(_middleware => {
      _middleware(store, action);
    });

    dispatch(action);
  } catch (err) {
    console.error('error: ', err)
  }
};

module.exports = {
  exceptionMiddleware,
  logMiddleware,
  timeMiddleware
};
```

> 使用

```javascript
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}));
const _dispatch = store.dispatch;
// 中间件注入
store.dispatch = exceptionMiddleware(logMiddleware, timeMiddleware)(store, _dispatch);

// 订阅
store.subscribe(() => {
  console.log("state", store.getState());
});

// 触发
store.dispatch({type: "reduce"});
store.dispatch({type: "add"});
store.dispatch({type: "add"});
store.dispatch({type: "blue"});
```

存在的问题: 未满足开封即用,增加中间件每次都需要写非业务代码

------

#### 封装新的createStore

中间件由我们提供,在生成store时注入即可,dispatch的修改在内部完成

> createNewStore.js

```javascript
const createNewStore = createStore => (...middleware) => reducer => {
  const exceptionMiddleware = (...middleware) => (store, dispatch) => action => {
    try {
      middleware.forEach(_middleware => {
        _middleware(store, action);
      });

      dispatch(action);
    } catch (err) {
      console.error('error: ', err)
    }
  };
  const _store = createStore(reducer);
  const _dispatch = _store.dispatch;
// 中间件更改
  _store.dispatch = exceptionMiddleware(...middleware)(_store, _dispatch);
  return _store;
};

module.exports = {
  createNewStore
};
```

> 拓展的中间件 middleware.js

```javascript
const logMiddleware = (store, action) => {
  console.log('action', action);
  console.log('last state', store.getState());
};

const timeMiddleware  = (store, action) => {
  console.log('time', Date.now());
  console.log('last state', store.getState());
};

module.exports = {
  logMiddleware,
  timeMiddleware
};
```

> 使用

```javascript
const store = createNewStore(createStore)(logMiddleware, timeMiddleware)(combineReducers({
  number: numberReducer,
  color: colorReducer
}));

// 订阅
store.subscribe(() => {
  console.log("state", store.getState());
});

// 触发
store.dispatch({type: "reduce"});
store.dispatch({type: "add"});
store.dispatch({type: "add"});
store.dispatch({type: "blue"});
```

---

#### 优化实现

- 根据最小开放原则,中间件需要的只是store上的getState方法
- 统一createStore和createNewStore,将createStore在内部封装为一个

> _createStore.js

```javascript
const { createStore } = require("./createStore");

const _createStore = (reducer, ...middleware) => {
  const exceptionMiddleware = (...middleware) => (getState, dispatch) => action => {
    try {
      middleware.forEach(_middleware => {
        _middleware(getState, action);
      });

      dispatch(action);
    } catch (err) {
      console.error('error: ', err)
    }
  };
  const _store = createStore(reducer);
  const getState = _store.getState;
  const _dispatch = _store.dispatch;
  // 中间件更改
  if (middleware) {
    _store.dispatch = exceptionMiddleware(...middleware)(getState, _dispatch);
  }
  return _store;
};

module.exports = {
  _createStore
};
```

> middleware.js

```javascript
const logMiddleware = (getState, action) => {
  console.log('action', action);
  console.log('last state', getState());
};

const timeMiddleware  = (getState, action) => {
  console.log('time', Date.now());
  // console.log('last state', getState());
};

module.exports = {
  logMiddleware,
  timeMiddleware
};
```

> 使用

```javascript
const { numberReducer } = require("./numberReducer");
const { colorReducer } = require("./colorReducer");
const { logMiddleware, timeMiddleware } = require("./middleware");
const { createStore, combineReducers } = require("./redux-9");

// 创建带中间件的store
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}), timeMiddleware, logMiddleware);

// 订阅
store.subscribe(() => {
  console.log("state", store.getState());
});

// 触发
store.dispatch({type: "reduce"});
store.dispatch({type: "add"});
store.dispatch({type: "add"});
store.dispatch({type: "blue"});
```

到此为止,一个类似redux的状态管理库就已经实现了

----

#### 支持替换Reducer

更改最基本的createStore方法即可

> createStore.js

```javascript
const createStore = reducer => {
  let state =  {};
  const listeners= [];

  const subscribe = listener => listeners.push(listener);
  const dispatch = action => {
    state = reducer(action.type);
    listeners.forEach(listener => listener());
  };

  dispatch({type: Symbol()});

  // 替换reducer
  const replaceReducer = newReducer => {
    reducer = newReducer;
    dispatch({ type: Symbol() })
  };

  const getState = () => {
    return state;
  };

  return {
    subscribe,
    dispatch,
    getState,
    replaceReducer
  }
};


module.exports = {
  createStore
};
```

> 使用

```javascript
const store = createStore(combineReducers({
  number: numberReducer,
  color: colorReducer
}), timeMiddleware, logMiddleware);

store.replaceReducer(numberReducer);
```

[全过程代码](https://github.com/dawangong/some-record/tree/master/redux%E5%AE%9E%E7%8E%B0)

