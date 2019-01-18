# Render props例子

## custom.vue

```vue
<template>
  <div>
     <Expand v-for="(item, index) in info.areaPosition" :createElementFun="createElement" :item="item" ></Expand>
  </div>
</template>
```



```vue
<script>
  export default {
    methods:{
      hideMsg(data){
        console.log(2)
      },
      createElement(h,name) {
       let functionalButtonArea = h('btn-group',{
          'style':{
            'color':'red'
          },
          'props':{
            'areaInfo':this.functionalButtonArea
          },
         'on':{
            'hideMsg':this.hideMsg
         }
        },'');
       return functionalButtonArea
      },
    },
    components: {
      Expand: {
        functional: true,
        props: {
          createElementFun: Function,
          item:Object
        },
        render: (h, ctx) => {
          let y = ctx.props.createElementFun(h,ctx.props.item.name)
          return h('div',[y]);
        }
      }
    },
  }
</script>

```

## btn-group.vue

```vue
<template>
  <div  class="btn clearfix block">
    <button v-for="(btnItem, index) in areaInfo.list" :key="index" :class="[`style${btnItem.style}`]" @click="hideMsg(index)">{{btnItem.value}}</button>
  </div>
</template>
<script>
export default{
    name:"BtnGroup",
    props:{
      areaInfo:{
            type:Object,
            default(){
                return {};
            }
        }
    },
    methods:{
        hideMsg(index){
            this.$emit('hideMsg',index)
        }
    }
}
</script>
```

