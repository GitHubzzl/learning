## minxin demo

### example.vue

```vue
<script>
    import { mapState } from 'vuex';
    import mixin from '../../assets/js/mixin.js'
    export default{
        name: '',
        mixins: [mixin],
        data(){}
    }
</script> 
```



### mixin.js

```javascript
import { mapState } from 'vuex';
var mixin = {
  computed: {
    ...mapState(["webUiInfo","printTable"]),
  },
  mounted() {
    window.addEventListener("resize", this.onWindowResize);
    this.onWindowResize();
  },
  methods: {
    /**
     * 页面尺寸调整
     */
    onWindowResize() {
      //获取表格距离顶部的距离
      var offsetTopValue = this.$el.querySelector(".tableInfoBox").getOffset().top;
      //获取窗口可视区域
      var innerHeight = window.innerHeight;
      //计算最小高度
      var minHeight = innerHeight - offsetTopValue - this.webUiInfo.body.margin.bottom;
      minHeight = (minHeight < 200) ? 200 : minHeight;
      //设置表格最小高度
      this.$el.querySelector(".tableInfoBox").style.minHeight = minHeight + "px";
      this.$el.querySelector(".tableInfoBox .ivu-table-tip span").style.minHeight = (minHeight - 100) + "px";
    },
  },
  destroyed() {
    window.removeEventListener("resize", this.onWindowResize);
  }
}

module.exports = mixin;
```



​	