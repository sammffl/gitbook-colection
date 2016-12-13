# Animated API

`Animated` 给我们三个动画组件：
- `Animated.View`
- `Animated.Text`
- `Animated.Image`
- 以及可以通过 `Animated.createAnimatedComponent`创建动画组件



## 创建一个可以被动画处理的值
Animated.Value: 单个值
```javascript
new Animated.Value(0)
```
Animated.ValueXY: 向量值
```javascript
new Animated.ValueXY({x:0, y:0}})
```
修改动画值通过setValue来处理
```javascript
...
constructor(props) {
    super(props);
    this.state = {
        translateValue: new Animated.ValueXY({x:0, y:0}), // 二维坐标
    };
}
resetAnimation() {
    this.state.translateValue.setValue({x:0, y:0});
}
...
```

## 动画的类型
* `spring`: 基础的单次弹跳物理模型
    * `friction`：摩擦力，默认为7
    * `tension`：张力，默认40
* `timing`: 从时间范围映射到渐变的值
    * `duration`：动画持续时间（单位是毫秒），默认500
    * `easing`：使用`Easing`api，来实现动画函数
    * `delay`：在一段时间之后开始动画（单位是毫秒），默认为0
* `decay`: 以一个初始速度开始并逐渐减慢停止
    * `velocity`：起始速度，必填参数
    * `deceleration`：速度衰减比例，默认为0.997

```javascript
startAnimation() {
    this.state.fadeAnim.setValue(0)
    this.fadeIn = Animated.timing(
        this.state.fadeAnim,
        {
            toValue: 1,
            duration: 3000,
            easing: Easing.linear,
        }
    ).start();
}
```

## 插值函数
将输入值范围转换为输出值范围
```javascript
...
style={[styles.animateView,{
    transform: [
        {
            rotate: this.state.rotateValue.interpolate({
                inputRange: [0, 1],
                outputRange: ['0deg', '360deg']
            })
        }
    ]
}]}
...
```

## 组合动画
* parallel（同时执行）
* sequence（顺序执行）
* stagger（错峰，插入了delay的parrllel）
* delay（组合动画之间的延迟方法）

## 循环执行动画
`start`方法可以接受一个函数，通过监听动画结束，在调用`startAnimation`可以重复执行动画

## 监听当前的动画值
* `addListener(callback)`：动画执行过程中的值
* `stopAnimation(callback)`：动画执行结束时的值

```javascript
this.state.rotateValue.addListener((state) => {   
    console.log("rotateValue=>" + state.value);
});
this.state.rotateValue.stopAnimation((state) => {   
    console.log("rotateValue=>" + state.value);
});
```
