<template>
    <!-- 问题：我们不知道什么时候能够拿到 max 值，因为max值是父组件通过异步请求获取商品信息拿到的，
              所以有时候，max值为undefined，
              但是，总归有一刻会拿到真正的 max值
         解决：我们可以使用 watch 属性监听，来监听 父组件传递过来的max值，
              不管watch会被触发几次，但是最后一次，肯定是一个合法的 max数值
    -->
    <div class="mui-numbox" data-numbox-min='1' :data-numbox-max='max'>
        <button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
        <input id="test" class="mui-input-numbox" type="number" value="1"
          @change="countChanged" ref="numbox" />
        <button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
    </div>

    <!-- 分析：子组件什么时候 把数据传给父组件 -->
</template>

<script>
    import mui from '../../lib/mui/js/mui.min.js'

    export default {
        name: "goodsinfo_numbox",
        props:['max'],
        watch:{
            /**
             * 属性监听
             * 解决思路：因为max的值总有一刻会到来，如果监听到了max的改变（即值到来了），
             *          则将 选择框的最大值设置成 max的值
             */
            'max': function (newVal, oldVal) {
                mui(".mui-numbox").numbox().setOption('max',newVal)
            }
        },
        mounted(){
            // 初始化 数字选择框 组件
            mui(".mui-numbox").numbox();
        },
        methods:{
            countChanged(){
                // 每当 文本框的数据被修改的时候，立即把 最新的数据 通过事件调用，传递给父组件
                // console.log(this.$refs.numbox.value)
                this.$emit('getCount',parseInt(this.$refs.numbox.value));
            }
        }
    }
</script>

<style scoped>

</style>