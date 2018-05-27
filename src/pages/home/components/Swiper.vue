<template>
    <div class="wrapper">
      <swiper :options="swiperOption">
        <swiper-slide v-for="item of swiperList" :key="item.id">
            <img class="swiper-img" :src="item.imgUrl" />
        </swiper-slide>
        <div class="swiper-pagination"  slot="pagination"></div>
      </swiper>
    </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [{
        id: '0001',
        imgUrl: 'https://img1.qunarzz.com/vc/56/c2/bc/94cd92692289c78770403648b5.jpg'
      }, {
        id: '0002',
        imgUrl: 'https://img1.qunarzz.com/vc/6a/36/df/4415fc5ed7c08d33649807f321.jpg'
      }, {
        id: '0003',
        imgUrl: 'https://img1.qunarzz.com/vc/84/65/6b/201b5b5c3462eeeda46c498225.jpg'
      }]
    }
  }
}
</script>

<style lang="stylus" scoped>
.wrapper >>> .swiper-pagination-bullet-active
  background: #fff
.wrapper
  overflow: hidden
  width: 100%
  height: 0
  padding-bottom: 31.25%
  background: #eee
  .swiper-img
    width: 100%
</style>
