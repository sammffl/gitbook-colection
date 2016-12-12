# 实现动画的几种方法

 - setState
 - setNativeProps
 - LayoutAnimation
 - Animated


> - `setState` 通过循环改变状态来触发render进行重新渲染来达到动画的效果
> - `setNativeProps` 会直接修改组件底层特性，不会重绘组件，因此性能也远胜动态修改组件内联style的方法。
> - 用于全局布局动画的 `LayoutAnimation`
> - 用于创建更精细的交互控制的动画 `Animated`

在react native里面，实现动画效果本质上就是改变组件的样式，通过不断的重新渲染组件达到动画的效果

除了常用的 Opacity、width、height、padding、margin...
还有一些常用的变换属性

```javascript
{
    ...
    width:10,
    transform:[
        // 缩放
        {scale: 1},
        {scaleX: 1},
        {scaleY: 1},
        // 移动
        {translateX: 1},
        {translateY: 1},
        // 旋转
        {rotate: '0deg'},
        {rotateX: '0deg'},
        {rotateY: '0deg'},
    ],
    ...
}
```
