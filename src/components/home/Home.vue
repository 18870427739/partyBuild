<!--Created by fjl on 2017/8/1-->
<!--首页-->
<template>
  <div class="home">
    <!--轮播图-->
    <viwe-pager :data="swipeData" @clickPic="goViwePagerDetail"></viwe-pager>
    <!--多列布局-->
    <much-col-layout :data="muchColData" @clickItem="goMuchColContent"></much-col-layout>
    <img class="img3" src="../../assets/img/homePage/banner01.png" alt="">
    <div class="div2">
      <a href=""></a><a href=""></a> <a href=""></a><a href="#/comments"></a><a href=""></a>
    </div>
  </div>
  <!--<head-nav>

  </head-nav>-->
</template>

<script>
  import muchColData from '../../appConfig/homeMuchSelect'
  import ViwePager from '../common/viwePager/ViwePager'
  import MuchColLayout from '../common/muchColLayout/MuchColLayout'
  export default{
    name: 'home',
    components: { ViwePager, MuchColLayout },
    data () {
      return {
        newsType: 0,
        swipeData: null,
        muchColData: muchColData
      }
    },
    methods: {

      // 进入轮播图详情页
      goViwePagerDetail (newsId) {
        this.$router.push({ name: 'NewsDetail', params: {title: '轮播图详情', type: this.newsType, id: newsId} })
      },
      // 进入多列布局内容
      goMuchColContent (index) {
        this.$router.push(muchColData[index].path)
      },
      // 请求轮播图片
      reqSwipe () {
        var param = {
          page: 0,
          rows: '5',
          type: 0
        }
        var _this = this
        this.$http.getNewsList(param).then(function (res) {
          var data = res.data
          _this.swipeData = data.rows
        })
      }
    },
    created () {
      this.reqSwipe()
    }
  }
</script>

<style scoped lang="less">
  .div2 {

    background: url("../../assets/img/homePage/specialColumn.png");
    width: 100%;
    height: 180px;
    margin-top: -4.7px;
    background-size: 100% 180px;
    a{
      width: 33.33%;
      height:50%;
      float: left;
    }
    a:nth-child(1){
      height:100%;
    }
  }
 .img3{
   width:100%;
 }
</style>

