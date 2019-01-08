<template>
    <div class="heard">
        <x-header :left-options="{backText: ''}">{{msg}}</x-header>
    </div>
</template>
<script>
import { XHeader } from 'vux'
document.documentElement.style.fontSize = document.documentElement.clientWidth / 7.5 + 'px'
export default {
  name: 'Head',
  components: {
    XHeader
  },
  props: ['msg'],
  data () {
    return {
    }
  },
  mounted () {},
  methods: {}
}
</script>
<style lang="less" scoped>
.heard {
  z-index: 2;
  display:block;
  width: 100%;
  .vux-header {
    background-color: #FFF;
    height: 1,28rem;
    border-bottom: 0.02rem solid #D2D2D2 ;
  }
}
</style>
<style lang="less">
.vux-header-title {
      color: black !important;
      height: 1.28rem !important;
      line-height:1.28rem !important;
      font-size: 0.36rem !important;
    }
    .vux-header .vux-header-left .left-arrow:before {
      border-color: #259BEC !important;
      border-width:0.04rem 0 0 0.04rem !important;
      width: 0.37rem !important;
      height: 0.37rem !important;
      top:0.40rem !important;
      left:0.43rem !important;
    }
</style>
