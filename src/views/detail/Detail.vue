<template>
    <div class="detail">
       <detail-nav-bar/>
        <scroll class="content">
            <detail-swiper :top-images="topImages"/>
            <detail-base-info :goods="goods"/>
            <detail-shop-info :shop="shop"/>
            <detail-image-info :detailInfo="detailInfo"/>
            <detail-params-info :paramsInfo="paramsInfo"/>
            <detail-comment-info :commentInfo="commentInfo"/>
        </scroll>
    </div>
</template>

<script>
import DetailNavBar from './childComponents/DetailNavBar'
import DetailSwiper from './childComponents/DetailSwiper'
import DetailBaseInfo from './childComponents/DetailBaseInfo'
import DetailShopInfo from './childComponents/DetailShopInfo'
import DetailImageInfo from './childComponents/DetailImageInfo'
import DetailParamsInfo from './childComponents/DetailParamsInfo'
import DetailCommentInfo from './childComponents/DetailCommentInfo'
import Scroll from 'components/common/scroll/Scroll'

import {getDetail, Goods, Shop} from "../../network/detail";

export default {
  name: 'Detail',
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      paramsInfo: {},
      commentInfo: {}
    }
  },
  created() {
    //保存传入的id
    this.iid = this.$route.params.id
    //根据iid请求详情数据
    getDetail(this.iid).then(res => {
      const data = res.result
      // console.log(data.itemParams)
      //获取顶部轮播
      this.topImages = data.itemInfo.topImages
      //获取商品信息
      this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
      //获取店铺信息
      this.shop = new Shop(data.shopInfo)
      //获取详情的信息
      this.detailInfo = data.detailInfo
      //获取参数的信息
      this.paramsInfo = data.itemParams
      //获取评论信息
      if (data.rate.cRate !== 0) {
        this.commentInfo = data.rate.list[0]
      }
    })
  },
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    DetailImageInfo,
    DetailParamsInfo,
    DetailCommentInfo,
    Scroll
  }
}
</script>

<style scoped>
.detail {
    height: 100vh;
    background-color: #fff;
    position: relative;
    z-index: 1;
}
.content {
    background-color: #ffffff;
    height: calc(100% - 44px);
}
</style>
