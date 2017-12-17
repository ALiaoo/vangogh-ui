# vangogh-ui

> A Vue.js project.

## Introduction
用vue封装一个自定义的checklist组件, 目的一是为了补充巩固一些vue的知识点, 二是梳理写一个组件的思路

### 效果展示


### 思路
*   确定组件效果,都有哪些功能.checklist的主要功能点有
    *  显示, 隐藏
    *  列表展示,从父组件接收一个list展示列表,超过最大高度可以滚动
    *  列表项有选中和非选中状态,选中操作会实时关联选中数目的变化
    *  选中结束,点击确定按钮把选中结果返回给父组件
*   定义Attributes，Events
*   划分dom结构,写出UI的基本骨架,比如用div来暂时把几个模块展示区分出来
*   开始依次细化每个模块,比如添加模块下的具体元素和css样式
*   实现交互.
*   数据渲染和事件传递.父子组件间的通信.

### Attributes
| 参数 | 说明 | 类型 |
|---------- |-------- |---------- |
| data | 数据列表 | array |
| max | 最多可选 | number |
    
### Events
| 事件名称 | 说明 | 回调参数 |
|---------- |-------- |---------- |
| onChange | 点击确定按钮时候触发的回调 | value | 
    
## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```
For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
