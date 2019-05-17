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

	</div>
</template>

<script>
import { NavBar } from 'vant';
import { HOME_module } from '@/api/shop';

import loadMore from '@/vue/mixin/list-load-more';
import scrollFixed from '@/vue/mixin/scroll-fixed';

export default {
  mixins: [loadMore, scrollFixed],

  data() {
    return {
      advertiseList: null,
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
      });
    }
  },
  components: {
    [NavBar.name]: NavBar
  }
};
</script>
