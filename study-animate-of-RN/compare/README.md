# 优缺点

* setState
* setNativeProps
* LayoutAnimation
* Animated

> `setState`: 性能损耗严重且动画比较生硬

> `setNativeProps`: 直接修改底层特性，不会重回组件，性能上远胜setState。但同样无法处理复杂动画，并且和动画相关的状态维护困难

> `LayoutAnimation`: 直接在Native实现一些动画效果，然后由JavaScript进行设置调用，由于整个动画过程交由Native处理。但是只有预置的几个动画效果。对于自定义动画、跟手动画没法实现

> `Animated`: 处理灵活，可实现复杂动画。但是在处理复杂业务同时进行动画会出现卡顿、掉帧（动画每帧超过16ms）
