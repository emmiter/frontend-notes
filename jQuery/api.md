01-[.one()](http://api.jquery.com/one/)

描述: 为某个元素的某种事件添加事件处理程序。每个元素每个事件类型的事件处理程序最多只会被执行一次。

```
.one(events,[,data],handler)
```

`events`: `String` 一个包含一个或多个javascript事件类型的字符串，比如"click","submit",或者自定义事件名字。

`data`:`PlainObject` 要传递给事件处理程序的数据对象

`handler`:`Function (Event eventObject)` 事件触发时执行的函数

