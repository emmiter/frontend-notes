## [Touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events)

为了提供高品质的基于触摸的用户接口，触摸事件提供了解释触摸屏或触控板上手指活动的行为。

当手指或输入笔首次碰触接触面时，多触摸(muti-touch)交互就开始了。其它手指可能也会接触触摸屏，也会沿着触摸界面移动。当用户手指从界面上移开时，交互才会停止。在交互过程中，应用程序会在开始阶段，移动阶段和终止阶段接收到触摸事件(touch events)

触摸事件和鼠标事件是很相似的。except they support simultaneous touches and at different locations on the touch surface.[TouchEvent](https://developer.mozilla.org/en-US/docs/Web/API/TouchEvent) 接口封装了封装了当前处于激活状态的所有touch points. [Touch](https://developer.mozilla.org/en-US/docs/Web/API/Touch) 接口，代表了一个单独的触摸点，包括相对于浏览器视口的该触摸点的位置信息。

接口:

* [TouchEvent](https://developer.mozilla.org/en-US/docs/Web/API/TouchEvent)

  当界面上的触摸状态改变时，就会触发该事件。

* [Touch](https://developer.mozilla.org/en-US/docs/Web/API/Touch)

  代表用户和触摸屏之间一个单独的接触点

* [TouchList](https://developer.mozilla.org/en-US/docs/Web/API/TouchList) 

  代表一组触摸点；用于用户的多个手指同时接触到了触摸屏

## [TouchEvent接口](https://developer.mozilla.org/en-US/docs/Web/API/TouchEvent)

1. Constructor

   `TouchEvent()`

2. Properties

   `TouchEvent.altkey`:

    A [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean) value indicating whether or not the alt (Alternate) key is enabled when the touch event is created. If the alt key is enabled, the attribute's value is `true`. Otherwise, it is `false`.

   `TouchEvent.changedTouches`:

   一个`TouchList`，触摸点对象会根据事件类型不同而不同，遵循如下规则:

   * 对于`touchstart`事件，是一系列处于当前事件的激活状态的触摸点
   * 对于`touchmove`事件，是自上一次触发事件到这次事件之间变化的触摸点
   * 对于`touchend`事件，是一系列已经从屏幕上移除的触摸点(也就是说，手指最后停留在屏幕上的触摸点集合)

   `TouchEvent.ctrlKey`

   `TouchEvent.metaKey`

   `TouchEvent.shiftKey`

   *`TouchEvent.targetTouches`*

   A [`TouchList`](https://developer.mozilla.org/en-US/docs/Web/API/TouchList) listing all the [`Touch`](https://developer.mozilla.org/en-US/docs/Web/API/Touch) objects for touch points that are still in contact with the touch surface **and** whose `touchstart` event occurred inside the same target [`element`](https://developer.mozilla.org/en-US/docs/Web/API/Element) as the current target element.

   `TouchEvent.touches`

   A [`TouchList`](https://developer.mozilla.org/en-US/docs/Web/API/TouchList) listing all the [`Touch`](https://developer.mozilla.org/en-US/docs/Web/API/Touch) objects for touch points that are currently in contact with the touch surface, regardless of whether or not they've changed or what their target element was at `touchstart`time.

   ### [Touch 接口](https://developer.mozilla.org/en-US/docs/Web/API/Touch)

   1. Constructor

      `Touch`

   2. Properties

      1. **Touch.clientX** — 返回触摸点相对于视口的X坐标，不包括任何的滚动偏移
      2. **Touch.clientY** — 返回触摸点相对于视口的Y坐标，不包括任何的滚动偏移
      3. **Touch.identifier** — 返回触摸点的唯一标识,This value remains consistent for every event involving this finger's (or stylus's) movement on the surface until it is lifted off the surface.
      4. **Touch.pageX** — 返回触摸点相对于视口的X坐标，包括任何的滚动偏移
      5. **Touch.pageY**— 返回触摸点相对于视口的Y坐标，包括任何的滚动偏移
      6. **Touch.screenX**— 返回触摸点相对于屏幕的X坐标，不包括任何滚动
      7. **Touch.screenY** — 返回触摸点相对于屏幕的Y坐标，不包括任何滚动
      8. **Touch.target**— Returns the [`Element`](https://developer.mozilla.org/en-US/docs/Web/API/Element) ([`EventTarget`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)) on which the touch contact started when it was first placed on the surface, even if the touch point has since moved outside the interactive area of that element or even been removed from the document. Note that if the target element is removed from the document, events will still be targeted at it, and hence won't necessarily bubble up to the window or document anymore. If there is any risk of an element being removed while it is being touched, the best practice is to attach the touch listeners directly to the target.
      9. ex **Touch.force** — 获取压力值
      10. ex **Touch.radiusX 和 **Touch.radiusY**
      11. ex **Touch.radiusY**