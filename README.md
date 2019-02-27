>  本项目是基于vue2最新实战项目，vue2 +vue-router2 + es6 +webpack 高仿饿了么app

### 项目页面预览

##### 店铺首页、公告页面、购物车页面

![外卖01_商品页11](E:\web前端\2019黑马\饿了么\资料\resource--更多资源q3190343277\resource\外卖01_商品页11.jpg)

##### 商品详情页面、店铺评价页面、商家详情页面

![外卖04_商品页面_商品详情111](E:\web前端\2019黑马\饿了么\资料\resource--更多资源q3190343277\resource\外卖04_商品页面_商品详情111.jpg)



### 开发目的

通过本项目的开发，巩固学到的关于vue +vue-router + es6 +webpack 等知识，提高自己的相关技术能力



### 技术栈

**前端**

- `Vue`：用于构建用户界面的 MVVM 框架
- `vue-router`：为单页面应用提供的路由系统，使用了 `Lazy Loading Routes` 技术来实现异步加载优化性能
- `vuex`：Vue 集中状态管理，在多个组件共享某些状态时非常便捷
- `vue-lazyload`：实现图片懒加载，节省用户流量，优化页面加载速度
- `better-scroll`：解决移动端各种滚动场景需求的插件，使移动端滑动体验更加流畅
- `SCSS`：css 预编译处理器
- `ES6`：ECMAScript 新一代语法，模块化、解构赋值、Promise、Class 等方法非常好用

**其他工具**

- `vue-cli`：Vue 脚手架工具，快速初始化项目代码
- `eslint`：代码风格检查工具
- `iconfont` ：阿里巴巴图标库
- `fastclick` ：消除 click 移动游览器 300ms 的延



### 实现功能

店铺首页、店铺公告页面、购物车页面、加入购物车、清空购物车、商品详情页面、商品评价页面、评价条件删选功能、商家详情页面等功能

##### 首页头部组件

- 弹层制作 [vue动画效果配置和弹层css sticky footer原理](https://segmentfault.com/a/1190000009281828)
  - 使用css sticky footer技术
  - vue的v-for遍历
  - vue的v-show和事件监听
  - vue动画处理
- header和公告栏制作
  - text-overflow:ellipsis的使用
  - font-size:0和vertical-align的使用
  - mixin的运用 [stylus相关和1像素边框问题](https://segmentfault.com/a/1190000009279775)
  - 背景图片的虚化
  - flex布局的使用

##### 商品区域

- 定义了2个wrapper,分别是menu-wrapper和foods-wrapper,对应当前页面的架构,左右两边的区域
- v-if和v-show的选择使用
- v-for传递索引
- vue传递原生事件$event
- 使用stylus的mixin处理一些border和img的问题
- 建立menu区域和foods区域的Y坐标对应关系,实现滚动foods区域会显示相应的menu区域,点击某个menu区域就显示某个固定的foods区域
- flex布局的使用,实现foods区域的布局
- 技巧类:对一些需要js操作的class(但是又没有实际用途的)可以建立一个类似food-list-hook钩子类
- font-size为0的技术点,处理行内元素的间隙问题
- vue的$nextTick使用
- vue的$refs的使用
- vue的computed属性使用
- vue的class绑定使用
- 在一些地方里面,使用table的垂直居中会很简单实现垂直居中
- better-scroll的使用

##### 购物车页面

绑定清空按钮

```
<div class="list-header">
            <h1 class="title">购物车</h1>
            <!--绑定empty方法清空购物车内容-->
            <span class="empty" @click="empty">清空</span>
</div>
```

通过设置selectFoods里面所有数据的count为0来实现清空的目的

```
empty() { //清空购物车内容
        this.selectFoods.forEach((food) => {
          food.count = 0;
        });
      },
```

##### 添加到购物车

- 生成一个动画小球的div,并且生成五个小球,五个是为了生成一定数量的小球来作为操作使用,按照小球动画的速度,一般来说五个也可以保证有足够的小球数量来运行动画
- 动画的内容分别是外层和内层,外层控制动画小球的轨道和方向,内层控制动画小球的运行状态
- 动画使用[vue的js钩子实现](http://cn.vuejs.org/v2/guide/transitions.html#JavaScript-)
- 因为小球动画只有一个方向(只执行单方向从上到下滚落),所以只用了before-enter,enter,after-enter
- 用v-show控制小球的可见性,在动画执行期间可见,其余时候隐藏

##### 商品详情页

```
<template>
  <transition name="move">
  <!--要实现这个商品详情页的内容滚动,所以需要有一个显示标志和一个dom绑定-->
  <div v-show="showFlag" class="food" ref="food">
  </div>
  </transition>
</template>
```

- 用ref绑定food的DOM元素,为了被bscroll做滚动处理
- 用transition包裹了整个food,为了实现这个页面的进入和退出动画

##### 

