# vue组件中的样式属性scoped

### Scoped CSS

> Scoped CSS规范是Web组件产生不污染其他组件，也不被其他组件污染的CSS规范。

vue组件中的style标签标有scoped属性时表明style里的css样式只适用于当前组件元素 
它是通过使用PostCSS来改变以下内容实现的:

```vue
<style scoped>
.example {
  color: red;
}
</style>

<template>
  <div class="example">hi</div>
</template>
```

渲染结果：

```vue
<style>
.example[data-v-f3f3eg9] {
  color: red;
}
</style>

<template>
  <div class="example" data-v-f3f3eg9>hi</div>
</template>
```

### 混合使用全局属性和局部属性

```vue
<style>
/* global styles */
</style>

<style scoped>
/* local styles */
</style>
```

### 关于子组件的根元素

使用了scoped属性之后，父组件的style样式将不会渗透到子组件中，然而子组件的根节点元素会同时被设置了scoped的父css样式和设置了scoped的子css样式影响，这么设计的目的是父组件可以对子组件根元素进行布局。 
.vue模板中的样式是根据需要按需加载，访问一个页面该组件中的样式就会追加到head标签中，如果父子组件中都对某个子组件根节点元素进行了控制，则父组件里的样式会被后来的覆盖。

### 深选择器

如果想对设置了scoped的子组件里的元素进行控制可以使用’>>>’或者’deep’

```vue
<template>
  <div id="app">
    <gHeader></gHeader>
  </div>
</template>

<style lang="css" scoped>
  .gHeader /deep/ .name{ //第一种写法
    color:red;
  }
  .gHeader >>> .name{   //二种写法
    color:red;
  }
</style>
<div class="gHeader">
  <div class="name"></div>
</div>
```

一些预处理程序例如sass不能解析>>>属性，这种情况下可以用deep，它是>>>的别名，工作原理相同。

### 动态生成的内容

使用v-html动态创建的DOM内容，不受设置scoped的样式影响，但你依然可以使用深选择器进行控制

参考文章

> scoped CSS官网 <https://vue-loader.vuejs.org/en/features/scoped-css.html> 
> 解决父组件无法修改子组件的问题 <https://zhuanlan.zhihu.com/p/29266022> 
> Scoped CSS规范 <https://github.com/AlloyTeam/AlloyTouch/wiki/Scoped-CSS>