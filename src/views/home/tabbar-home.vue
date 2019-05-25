<template>
	<div class="tab_home">

    <van-nav-bar
      title="标题"
      left-text="返回"
      right-text="按钮"
      left-arrow
    />

    <van-swipe :autoplay="3000" :height="200">
      <van-swipe-item v-for="(image, index) in advertiseList" :key="index">
        <img v-lazy="image.pic" height="200px" />
      </van-swipe-item>
    </van-swipe>

    <div style="margin-top: 20px">
      <van-cell title="品牌直供" value="更多" size="large" />
      <van-col span="12" v-for="brand in brandList" style="padding: 2px" >
        <van-card
          tag="上新"
          price="2.00"
          :title="brand.name"
          :thumb="brand.logo"
        >
        </van-card>
      </van-col>
   </div>


    <div style="margin-top: 20px">
      <van-cell title="新品推荐" value="更多" size="large" />
      <van-col span="12" v-for="product in newProductList" style="padding: 2px" >
        <van-card
          tag="上新"
          price="2.00"
          origin-price="10.00"
          :title="product.name"
          :thumb="product.pic"
        >
        </van-card>
      </van-col>
   </div>


    <div style="margin-top: 20px">
      <van-cell title="新品推荐" value="更多" size="large" />
      <van-col span="24" v-for="product in hotProductList" style="padding: 2px" >
        <van-card
          tag="热销"
          price="2.00"
          origin-price="10.00"
          :title="product.name"
          :thumb="product.pic"
        >
        </van-card>
      </van-col>
   </div>

	</div>
</template>

<script>
import { NavBar, Row, Col, Card, Panel,Cell } from 'vant';
import { HOME_module } from '@/api/shop';

import loadMore from '@/vue/mixin/list-load-more';
import scrollFixed from '@/vue/mixin/scroll-fixed';

export default {
  mixins: [loadMore, scrollFixed],

  data() {
    return {
      advertiseList: null,
      brandList: null,
      newProductList: null,
      hotProductList: null,
      isLoading: false
    };
  },

  created() {
    this.initViews();
  },

  methods: {
    initViews() {
      this.$reqGet(HOME_module).then(res => {
        this.advertiseList = res.data.data.advertiseList;
        this.brandList     = res.data.data.brandList;
        this.newProductList = res.data.data.newProductList;
        this.hotProductList = res.data.data.hotProductList;
      });
    }
  },
  components: {
    [NavBar.name]: NavBar,
    [Row.name]: Row,
    [Col.name]: Col,
    [Card.name]: Card,
    [Panel.name]: Panel,
    [Cell.name]: Cell,
  }
};
</script>
