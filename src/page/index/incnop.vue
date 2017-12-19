<template>
	<swiper :options="icfonOption">
      <swiper-slide v-for="(pageInfo, index) in pages" :key="index">
        <div class="icon-wrapper">
          <div v-for="item in pageInfo" :key="item.id" class="icon-item">
            <div class="icon-img-con">
              <img  class="icon-img" :src="item.imgUrl"/>
            </div>
            <p class="dev">{{item.title}}</p>
          </div>
        </div>
      </swiper-slide>
      <div class="icon-pagination"  slot="pagination"></div>
    </swiper>
</template>
<script>
export default {
  props: ['pages'],
  data () {
    return {
      icfonOption: {
        pagination: '.icon-pagination'
      }
    }
  }
}
</script>
<style scoped>
  .icon-pagination{
    text-align: center;
  }
  .icon-wrapper {

  }
  .icon-item {
    box-sizing: border-box;
    float: left;
    width: 25%;
    padding: .4rem;
  }
  .icon-img-con {
    width: 100%;
    height: 0;
    padding-bottom: 100%;
  }
  .icon-img {
    width: 100%;
  }
  .dev{
    font-size: 0.24rem;
    text-align: center;
    padding-top: 0.2rem
  }
</style>