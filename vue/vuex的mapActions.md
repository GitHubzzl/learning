# vuex的mapActions

### 方式一

在vuex的actions中定义一个方法：

```javascript
actions: {
    vuexSetTest({commit}, val){
        commit("vuex_set_test", val);
    }
}
```


调用时这样调用：

```javascript
this.$store.dispatch("vuexSetTest", "ttttttt");
```

------

### 方式二

mapActions的作用就是，把actions中的方法映射到methods中，换一种调用方式。

引入mapAction：

```javascript
import {mapActions,} from 'vuex'
```

映射方法：

```javascript
"methods": {
    ...mapActions([
        "vuexSetTest"
    ]),
}
```


调用方法：

```javascript
this.vuexSetTest("eeee")
```

用这种方式，通常，在actions里返回一个promise，这样可以this.vuexSetTest("eeee").then(res=>{})



------

### namespaced:true

如果命名空间为true，可以这样调用：

```javascript
export default {
  namespaced:true,
  actions:{}
}
```

```javascript
methods:{
      ...mapActions(['user/actionA']),
}
```

```
this['user/actionA']()
```





