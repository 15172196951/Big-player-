<template>
    <div class="setgiftSigning">
        <Head msg="签赠设置"/>
        <div class="box">
            这个高度设计稿上390px，
            我写的3.9rem,
            差距太大了吧！
        </div>
    </div>
</template>
<script>
import Head from './heard.vue'
export default {
  components: {
    Head
  },
  data () {
    return {
    }
  },
  mounted () {},
  methods: {}
}
</script>
<style lang="less">
    .setgiftSigning{
        display: block;
        width: 100%;
        background-color: aqua;
        .box{
            width: 100%;
            height: 3.9rem;
            background-color: yellow;
        }
    }
</style>


