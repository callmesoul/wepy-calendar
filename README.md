# 微信小程序 wepyjs 第三方 日历组件

![toast](http://nowechat.oss-cn-shenzhen.aliyuncs.com/TIM%E5%9B%BE%E7%89%8720180116113203.png)


## 说明

基本实现功能：
1. 日历显示
2. 选择时间
3. 打卡日期


## 使用

### 拷贝到components里
把 calender.wpy拷贝到组件文件夹里
### 引入组件
```javascript
// index.wpy
<template>
    <wepyCanlendar></wepyCanlendar>
</template>
<script>
    import wepy from 'wepy';
    import wepyCanlendar from '@/components/calendar'

    export default class Index extends wepy.page {
        components = {
            wepyCanlendar
        };
    }
    
</script>
```
### 自定义参数
```javascript
// index.wpy
<template>
    <wepyCanlendar 
        :currentDate.sync="currentDate" // 日历当前时间 默认为今天
        :startDate.sync="startDate" // 日历选择器picker的最小时间 默认为3年之前
        :endDate.sync="endDate" // 日历选择器picker的最大时间 默认为3年之后
        :hasIconList.sync="hasIconList" // 日历中显示的天数数组
    ></wepyCanlendar>
</template>
<script>
    import wepy from 'wepy'
    import wepyCanlendar from '@/components/calendar'

    export default class Index extends wepy.page {
        components = {
            wepyCanlendar
        };
        
        onLoad(){
            this.$broadcast("startRenderCalendar");//通知日历组件可以开始渲染
        }
        
        data = {
              currentDate: "2018-08-09",
              startDate: '2018-01-01',
              endDate: '2018-02-01',
              hasIconList:[ '2018-06-01', '2018-06-06', '2018-06-09', '2018-06-10', '2018-06-15' ]
        };  // 页面所需数据均需在这里声明，可用于模板数据绑定
        
        events = {
              calChangeCurrentMonth:function (date,e) {
                 //日历当前月份改变回调
              },
              calChangeSelectedDay:function (date,e) {
                //点击日历选择天回调
              }
            };  // 声明组件之间的事件处理函数
    }
    
</script>
```


| 属性/方法   | 必填    |  默认值  |备注|
| --------   | -----   | ---- |---- |
| currentDate | 否      |   new Date() |日历当前时间|
| startDate    否      |   null    |日历时间选择picker最小时间|
| endDate    | 否      |   null    |日历时间选择picker最大时间|
| hasIconList  | 否      |   []    |日历显示天数组|
| calChangeCurrentMonth  | 否      |   (date,e)    |日历当前月份改变回调
| calChangeSelectedDay  | 否      |   (date,e)    |声明组件之间的事件处理函数
| this.$broadcast("startRenderCalendar");  | 是      |   ‘’    |通知组件可以开始渲染


