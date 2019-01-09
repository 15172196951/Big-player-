<template>
    <div class="Staff">
        <Head msg="员工"/>
        <div>
          <div class="co-bg-0 co-flex contentbox1" @click="jumpDetail()">
                <img v-avatar="name"
                    class="round round-mg-06 fs-0" />
                <div class="co-bd-b content co-of fg-1" style="padding-top:0.23rem;padding-bottom:0.25rem;padding-right:0.32rem">
                    <p class="content-name co-te">我是姓名</p>
                    <p  class="content-address">华南区/啥子/嗯嗯</p>
                </div>
          </div>
        </div>
    </div>
</template>

<script>
import Head from "./heard.vue";
document.documentElement.style.fontSize =
  document.documentElement.clientWidth / 7.5 + "px";
export default {
  components: {
    Head
  },
  data() {
    return {
      name: "小化"
    };
  },
  mounted() {},
  methods: {
    jumpDetail() {
      console.log("被电击");
    }
  }
};
</script>

<style lang="less" scoped>
.Staff {
  display: block;
  width: 100%;
  height: 100%;
  .contentbox1 {
    margin-top: 0.02rem;
    margin-bottom: 0.02rem;
    font-size: 0.28rem;
    .round {
      border-radius: 100%;
      width: 0.72rem;
      height: 0.72rem;
    }
    .content-name {
      font-size: 0.28rem;
      color: #222222;
      line-height: 0.4rem;
      margin-bottom: 0.07rem;
    }
    .content-address {
      line-height: 0.37rem;
      font-size: 0.26rem;
      color: #888888;
    }
    .round-mg-06 {
      margin: 0.32rem 0.24rem 0.32rem 0.3rem;
    }
    .fs-0 {
      flex-shrink: 1; //缩小比例
    }
    .fg-1 {
      flex-grow: 1; //放大比例
    }
  }
}
</style>
<style lang="less">
.co-Page {
  // position: relative;
}
</style>


