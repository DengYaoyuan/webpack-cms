<template>
    <div>
        <!-- 轮播图区域 -->
        <mt-swipe :auto="3000">
            <mt-swipe-item>1</mt-swipe-item>
            <mt-swipe-item>2</mt-swipe-item>
            <mt-swipe-item>3</mt-swipe-item>
            <mt-swipe-item>4</mt-swipe-item>

            <!-- 由于现在无法获取数据，先注释 -->
            <!-- 在组件中，使用v-for循环的话，一定要使用key -->
            <!--<mt-swipe-item v-for="item in lunbotuList" :key="item.url">-->
                <!--<img :src="item.img" alt="">-->
            <!--</mt-swipe-item>-->
        </mt-swipe>
        <!-- 宫格区域 -->
        <ul class="mui-table-view mui-grid-view mui-grid-9">
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/home/newsList">
                    <img src="../../images/menu1.png"/>
                    <div class="mui-media-body">新闻资讯</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/home/photolist">
                    <img src="../../images/menu2.png"/>
                    <div class="mui-media-body">图片分享</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
                <router-link to="/home/goodslist">
                    <img src="../../images/menu3.png"/>
                    <div class="mui-media-body">商品购买</div>
                </router-link>
            </li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
                <img src="../../images/menu4.png"/>
                <div class="mui-media-body">留言反馈</div></a></li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
                <img src="../../images/menu5.png"/>
                <div class="mui-media-body">视频专区</div></a></li>
            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
                <img src="../../images/menu6.png"/>
                <div class="mui-media-body">联系我们</div></a></li>
        </ul>
        <h4>home</h4>
    </div>
</template>

<script>
    import { Toast } from 'mint-ui'

    export default {
        data(){
            return {
                lunbotuList:[]    // 保存轮播图的数组
            };
        },
        created(){
            this.getLunbotu();
        },
        methods:{
            getLunbotu(){
                // 获取轮播图数据的方法
                this.$http.get('http://vue.studyit.io/api/getlunbotu').then(result => {
                    console.log(result.body)
                    if (result.body.status === 0){
                        // 获取轮播图的数据成功
                        this.lunbotuList = result.body.message;
                    }else {
                        // 获取数据失败
                        Toast('加载轮播图数据失败。。。。')
                    }
                })
            }
        }
    }
</script>

<style lang="scss" scoped>
    .mint-swipe{
        height: 200px;
        .mint-swipe-item{
            &:nth-child(1){
                background-color: lightcoral;
            }
            &:nth-child(2){
                background-color: lightblue;
            }
            &:nth-child(3){
                background-color: lightgreen;
            }
            &:nth-child(4){
                background-color: lightsalmon;
            }
            img{
                width: 100%;
                height: 100%;
            }
        }
    }

    .mui-grid-view.mui-grid-9{
        background-color: #fff;
        border: none;
        img {
            width: 60px;
            height: 60px;
        }
        .mint-media-body{
            font-size: 13px;
        }
    }
    .mui-grid-view.mui-grid-9 .mui-table-view-cell{
        border: none;
    }

</style>