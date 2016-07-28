### [01-Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

**map()** 方法会创建一个新数组。原数组的每个元素将被传入回调函数，函数返回值则作为新数组的相应位置的新元素。

```javascript
arr.map(callback[,thisArg])
```

* `callback`

  产生数组新元素的函数，接收三个参数:

  * `currentValue` : 数组中正在被处理的值
  * `index` : 正在被处理的值的索引
  * 调用 map 方法的数组

* `thisArg`

  可选。执行回调的时候，被用作`this`的值，默认值是`window`对象。

  ​



