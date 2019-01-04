<template>
    <div class="heard">
        <x-header :left-options="{backText: ''}">{{msg}}</x-header>
    </div>
</template>
<script>
import { XHeader } from 'vux'
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
  display:block;
  width: 100%;
  .vux-header {
    background-color: #FFF;
    height: 3.2rem;
    
  }
}
</style>
<style lang="less">
.vux-header-title {
      color: black !important;
      height: 3.2rem !important;
      line-height:3.2rem !important;
      font-size: 0.9rem !important;
    }
    .vux-header .vux-header-left .left-arrow:before {
      border-color: #259BEC !important;
      margin-top:0.5rem;
    }
</style>
