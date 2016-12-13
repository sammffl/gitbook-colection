# setNativeProps方法
如果执意使用修改`state`的方式，觉得这种方式更符合当前需求对动画的控制，那么则应当使用原生组件的`setNativeProps`方法来做对应实现，它会直接修改组件底层特性，不会重绘组件，因此性能也远胜动态修改组件内联style的方法。

```javascript
...
animateSizeFunc(){
    requestAnimationFrame(() =>{

        if(this.count<50){
            ++this.count;
            this.refs.img.setNativeProps({
                style: {
                    width: this.state.width++,
                    height: this.state.height++,
                }
            });

            this.animateSizeFunc();
        }
    });
}
...
```

## 优点
`setNativeProps`直接修改组件底层特性，不会重绘组件，因此性能也远胜动态修改组件内联style的方法。
缺点：
1. `setNativeProps`属于原生视图的方法，如果我们使用一个动画，单纯只是为了跟踪它的值，那么这么方法有点不合时宜。
2. 还是和上面一种方式一样，如果需要实现‘弹性动画’，‘淡入淡出’等效果，则还是比较麻烦的。
