###HTML 元素

(<div>, <p>,<span>, <a>, etc.)都有指定的React组件。

React React Native React Native

<div> <View>

<span> <Text>

<li>, <ul> <ListView>

<img> <Image>

<View>组件 替代 <div>标签：

ios中渲染成一个UIView，Android中是一个View。

平台的特定元素：

<DatePickerIOS>表示 ios上的日期选择器

<DatePickerIOS

date={this.state.date}

mode="date"

timeZoneOffsetInMinutes={this.state.timeZoneOffsetInHours * 60}

/>

  
