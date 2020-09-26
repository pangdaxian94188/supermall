<template>
    <div id="detail" class="detail">
        <detail-nav-bar class="detail-nav"/>
        <scroll class="content">
            <detail-swiper :top-images="topImages" />
            <detail-base-info :goods="goodsInfo" />
            <detail-shop-info :shop="shopInfo"/>
            <detail-image-info :detail-info="detailInfo"  @imageLoad="imageLoad"/>
            <item-params-info :param-info="itemParams"/>
        </scroll>
    </div>
</template>

<script>
    import DetailNavBar from './childComps/DetailNavBar';
    import DetailSwiper from './childComps/DetailSwiper';
    import DetailBaseInfo from './childComps/DetailBaseInfo';
    import DetailShopInfo from './childComps/DetailShopInfo';
    import DetailImageInfo from './childComps/DetailImageInfo';
    import ItemParamsInfo from './childComps/ItemParamsInfo';

    import Scroll from '../../components/common/scroll/Scroll'

    import {
        getDetail,
        Goods
    } from '../../network/detail'
    export default {
        name: "Detail",
        components: {
            DetailNavBar,
            DetailSwiper,
            DetailBaseInfo,
            DetailShopInfo,
            DetailImageInfo,
            ItemParamsInfo,
            Scroll
        },
        data() {
            return {
                iid: null,
                topImages: [],
                goodsInfo: {},
                shopInfo:{},
                detailInfo:{},
                itemParams:{}
            }
        },
        created() {
            // 1.保存传入的iid
            this.iid = this.$route.params.iid
            // 2.根据iid请求详情数据
            getDetail(this.iid).then(res => {
                // 1.获取数据
                const data = res.result
                // 2.获取顶部的图片轮播数据
                this.topImages = res.result.itemInfo.topImages
                // 3.创建商品的对象
                this.goodsInfo = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
                // 4.取出店铺的信息
                this.shopInfo=data.shopInfo
                // 5.取出详情的信息
                this.detailInfo=data.detailInfo
                // 6.取出参数的信息
                this.itemParams=data.itemParams
            })
        },
    methods: {
      imageLoad() {
        this.$refs.scroll.refresh()
      }
    }
    }
</script>

<style>
  #detail {
    position: relative;
    z-index: 9;
    background-color: #fff;
    height: 100vh;
  }

  .detail-nav {
    position: relative;
    z-index: 9;
    background-color: #fff;
  }

  .content {
    height: calc(100% - 44px);
  }
</style>