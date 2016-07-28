[API和API引入](http://cn.redux.js.org/docs/api/index.html)

顶级暴露的方法

1. [createStore(reducer,[initialState])](http://cn.redux.js.org/docs/api/createStore.html)
2. [combineReducers(reducers)](http://cn.redux.js.org/docs/api/combineReducers.html)
3. [applyMiddleware(…middlewares)](http://cn.redux.js.org/docs/api/applyMiddleware.html)
4. [bindActionCreators(actionCreators,dispatch)](http://cn.redux.js.org/docs/api/bindActionCreators.html)
5. [compose(…functions)](http://cn.redux.js.org/docs/api/bindActionCreators.html)

Store API

Store

* [getState](http://cn.redux.js.org/docs/api/Store.html#getState)
* [dispatch(action)](http://cn.redux.js.org/docs/api/Store.html#getState)
* [subscrible(listener)](http://cn.redux.js.org/docs/api/Store.html#getState)
* [getReducer()](http://cn.redux.js.org/docs/api/Store.html#getState)
* [replaceReducer(nextReducer)](http://cn.redux.js.org/docs/api/Store.html#replaceReducer)

上面介绍的所有函数都是顶级暴露的方法。引入方式如下:

ES6

```javascript
import {createStore} from 'redux'
```

ES5(CommonJS)

```javascript
var createStore = require('redux').createStore
```

ES5(UMD build)

```javascript
var createStore = Redux.createStore
```

