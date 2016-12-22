# 使用react-native-scrollable-tab-view插件来实现tabView

```javascript
import ScrollableTabView, { DefaultTabBar } from 'react-native-scrollable-tab-view';
```

```javascript
<ScrollableTabView
    renderTabBar={(tabBarProps) =>{
        return (<DefaultTabBar />)
    }}
    tabBarPosition="top"
    onChangeTab={(i)=> {
        this.setState({
            scrollText: `{i:${i.i},from:${i.from}}`,
        })
    }}
    initialPage={1}
    tabBarUnderlineStyle={styles.underline}
    tabBarBackgroundColor={'green'}
    tabBarActiveTextColor={'yellow'}
    tabBarTextStyle={{fontSize:26}}
    // scrollWithoutAnimation={Boolean(true)}
>
    <View tabLabel='Tab #1' style={styles.flexBox}>
        <Text>1</Text>
        {!!this.state.scrollText&&<Text>onChangeTab => {this.state.scrollText}</Text>}
    </View>
    <View tabLabel='Tab #2' style={styles.flexBox}>
        <Text>2</Text>
        {!!this.state.scrollText&&<Text>onChangeTab => {this.state.scrollText}</Text>}
    </View>
    <View tabLabel='Tab #3' style={styles.flexBox}>
        <Text>3</Text>
        {!!this.state.scrollText&&<Text>onChangeTab => {this.state.scrollText}</Text>}
    </View>
</ScrollableTabView>
```
