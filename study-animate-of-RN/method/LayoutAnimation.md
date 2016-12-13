# LayoutAnimation API

当布局变化时，自动将视图运动到它们新的位置上

一个常用的调用此API的办法是调用`LayoutAnimation.configureNext`，然后调用`setState`。

## 创建`LayoutAnimation` 的配置文件
一个标准的config格式如下：(`create`、`update`和`delete`，分别表示视图创建、更新和删除时候的动画)
```javascript
LayoutAnimation.configureNext(
    {
        duration: 700, //持续时间
        create: { // 视图创建
            type: LayoutAnimation.Types.spring,
            property: LayoutAnimation.Properties.scaleXY,// opacity、scaleXY
        },
        update: { // 视图更新
            type: LayoutAnimation.Types.spring,
        },
    },
    function(){
        // alert(1)
    }
);

this.setState({
    width: this.state.width + 50,
    height: this.state.height + 50
});
```
其中`create`、`update`和`delete`的`Anim`格式如下
```javascript
type Config = {
  duration: number;
  create?: Anim;
  update?: Anim;
  delete?: Anim;
}

type Anim = {
  duration?: number; //动画时长
  delay?: number; //延时执行 毫秒
  springDamping?: number; // 弹跳动画阻尼系数（配合spring使用）
  initialVelocity?: number; //初始速度
  type?: $Enum<typeof TypesEnum>; //动画类型
  property?: $Enum<typeof PropertiesEnum>;// 处理类型
}

var TypesEnum = {
  spring: true, // 弹跳
  linear: true, // 线性
  easeInEaseOut: true, // 缓入缓出
  easeIn: true, // 缓入
  easeOut: true, //缓出
  keyboard: true, // 测试下来和linear动画效果类似
};

var PropertiesEnum = {
  opacity: true, // 透明度
  scaleXY: true, // 缩放
};
```



## LayoutAnimation 接口返回内容
* LayoutAnimation
    * create （简单的创建一个配置文件）
    ```javascript
    startAnimation() {
        LayoutAnimation.configureNext(
            LayoutAnimation.create(
                700,
                LayoutAnimation.Types.spring,
                LayoutAnimation.Properties.scaleXY
            )
        );
        this.setState({
            width: this.state.width + 10,
            height: this.state.height + 10
        });
    }
    ```
    * Types
        * easeIn
        * easeInEaseOut
        * easeOut
        * keyboard
        * linear
        * spring
    * Properties
        * opacity
        * scaleXY
    * configChecker
    * Presets （预设默认动画）
    ```javascript
    startAnimation() {
        LayoutAnimation.configureNext(LayoutAnimation.Presets.linear);
        this.setState({
            width: this.state.width + 10,
            height: this.state.height + 10
        });
    }
    ```
        * easeInEaseOut
        * linear
        * spring
    * easeInEaseOut
    ```javascript
    startAnimation() {
        LayoutAnimation.easeInEaseOut();
        this.setState({
            width: this.state.width + 10,
            height: this.state.height + 10
        });
    }
    ```
    * linear
    * spring
