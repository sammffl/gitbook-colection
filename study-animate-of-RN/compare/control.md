# 可控性

`setState`: 由于是不断更改state的，所以对追踪动画某一阶段的状态值不好处理

`setNativeProps`: 因为直接修改底层特性，不会改变state状态。所以对状态需要额外的监控

`layoutAnimation`: 在处理组合动画上有致命弱点，首先第二个参数是可以监听动画结束，但只在ios上有效。并且在组合动画上会形成回调地狱
```JavaScript
LayoutAnimation.configureNext(
    {
        duration: 700, //持续时间
        create: { // 视图创建
            type: LayoutAnimation.Types.keyboard,
            property: LayoutAnimation.Properties.scaleXY,// opacity、scaleXY
        },
        update: { // 视图更新
            type: LayoutAnimation.Types.keyboard,
        },
    },
    () =>{
        LayoutAnimation.easeInEaseOut();
        this.setState({
            width: this.state.width - 50,
            height: this.state.height - 50
        });
    }
);
```

`Animated`: 在可控性上最为灵活，从众多接口就可以看出，但是灵活也带来了性能上的问题，需要在处理动画的时候搭配StaticContainer组件使用，优化渲染性能。
