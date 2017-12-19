<template>
  <div>
    <header class="header">
      <div class="back iconfont">&#xe624;</div>
      <div class="search"><a href="#" class="prompt">输入城市/景点/游玩主题</a></div>
      <div class="city">城市</div>
    </header>
    <swiper-router :swiperInfo="swiperInfo"></swiper-router>
    <my-icon :pages="pages"></my-icon>
  </div>
</template>

<script>
  import SwiperRouter from './swiper'
  import myIcon from './incnop'

  export default {
    name: 'Index',
    components: {
      SwiperRouter,
      myIcon
    },
    data () {
      return {
        swiperInfo: [],
        iconInfo: [],
        around: []
      }
    },
    computed: {
      pages () {
        const pages = []
        this.iconInfo.forEach((value, index) => {
          let page = Math.floor(index / 8)

          if (!pages[page]) {
            pages[page] = []
          }
          pages[page].push(value)
        })
        return pages
      }
    },

    methods: {

      getIndexData () {
        this.$http.get('/static/index.json')
          .then(this.handleGetDataSucc.bind(this))
      },

      handleGetDataSucc (res) {
        const body = res.body
        if (body && body.data && body.data.swiper) {
          this.swiperInfo = body.data.swiper
          this.iconInfo = body.data.icons
          this.around = body.data.around
        }
      }

    },

    created () {
      this.getIndexData()
    }
  }
</script>

<style scoped>
  .header {
    display: flex;
    background: #05bad5;
    color: #fff;
  }
  .back {
    width: .64rem;
    line-height: .86rem;
    text-align: center;
  }
  .search {
    flex: 1;
    margin: .14rem .18rem;
    background: #fff;
    border-radius: .1rem;
  }
  .icon-shuaxin {
    color: #ccc;font-size: 0.26rem;padding:0 0.15rem;
  }
  .prompt {
    font-size: 0.26rem;color: #ccc;line-height: 0.6rem;
  }
  .city {
    width: 1.14rem;
    line-height: .86rem;
    text-align: left;
  }
  .city::after{
    content:"";
    display: block;
    width: 0px;
    height: 0px;
    border: 0.1rem solid #fff;
    border-color: white transparent transparent transparent;
    position: absolute;
    right: 0.3rem;
    top: 0.36rem;
  }
</style>
