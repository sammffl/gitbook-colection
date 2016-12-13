# setState方法

在不使用任何动画API，最简单粗暴的方式就是——通过修改`state`不断改变视图的样式

```javascript
...
this.state = {
    rotateValue: '0deg',
}
...
_renderRotate(){
    return (
        <View style={[styles.animateView,{
            transform:[
                {rotate:this.state.rotateValue}
            ],
        }]}>
            <Text style={{fontSize:20}}>requestAnimationFrame rotate</Text>
        </View>
    );
}
animateRotateFunc(){
    requestAnimationFrame(()=>{
        if(this.degree < 360){
            this.degree+=30;
            this.setState({
                rotateValue: `${this.degree}deg`
            });
            this.animateRotateFunc();
        }
    });
}
...
```

## 这个方式实现的动画有几个问题
1. 实现方式是通过不断销毁、创建视图来完成，一方面如果你的视图的数据是动态获取的，那么就需要以合适的方式恢复数据；另外一方面，这种方式必然造成性能和内存开销的问题。
2. 如果需要刷新的View的层级比较深，那么这种方式会带来严重的性能问题。
3. requestAnimationFrame毕竟是web上css的用法，在手机上，动画的效果比较生硬，如果需要‘弹性动画’，‘淡入淡出’等效果，则是比较难以实现的（需要辅助各种函数）。
