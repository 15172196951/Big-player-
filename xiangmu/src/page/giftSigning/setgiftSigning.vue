<template>
    <div class="setgiftSigning">
        <Head msg="签赠设置"/>
        <div class="shopSelect">
            安西李家村万达店
        </div>
        <div class="giftAdd co-flex co-jsb">
            <p>签赠人管理</p>
            <p @click="giftAdd">
                <img src="../../assets/images/add1.png" alt="#">
                <span>新增签赠人</span>
            </p>
        </div>
        <div class="contentbox">
            <div class="co-bg-0 co-flex contentbox1" @click="jumpDetail()">
                <img v-avatar="name"
                    class="round round-mg-06 fs-0" />
                <div class="co-bd-b content co-of fg-1" style="padding-top:0.23rem;padding-bottom:0.25rem;padding-right:0.32rem">
                    <p class="content-name co-te">我是新明</p>
                    <p  class="content-address">华南区/啥子/嗯嗯</p>
                </div>
            </div>
        </div>
        <div class="bj-dialog" v-if="showDialog">
            <div class="dialog-content">
                <p class="dialog-p1">编辑</p>
                <p @click="xiugai">修改签赠人</p>
                <p @click="detele">删除签赠人</p>
                <p @click="quxiao">取消</p>
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
      name: "小明",
      showDialog: false
    };
  },
  mounted() {},
  methods: {
    giftAdd() {
      this.$router.push({ path: "/giftSigning/new" });
    },
    xiugai() {
      console.log("修改被电击");
    },
    detele() {
      console.log("删除被电击");
    },
    quxiao() {
      this.showDialog = false;
    },
    jumpDetail() {
      this.showDialog = true;
    }
  }
};
</script>
<style lang="less" scoped>
.setgiftSigning {
  display: block;
  width: 100%;
  height: 100%;
  .shopSelect {
    height: 0.9rem;
    font-size: 0.28rem;
    margin-bottom: 0.3rem;
    padding-left: 0.4rem;
    line-height: 0.9rem;
  }
  .giftAdd {
    font-size: 0.3rem;
    padding: 0 0.3rem;
    height: 0.9rem;
    line-height: 0.9rem;
    img {
      vertical-align: top;
      width: 0.29rem;
      height: 0.29rem;
      margin-top: 0.29rem;
    }
  }
  .contentbox {
    height: 1.36rem;
    font-size: 0.28rem;
    .contentbox1 {
      margin-top: 0.02rem;
      margin-bottom: 0.02rem;
    }
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
  .bj-dialog {
    position: absolute;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #222222;
    background: rgba(0, 0, 0, 0.6);
    z-index: 1;
    .dialog-content {
      position: absolute;
      top: 5.31rem;
      left: 1.95rem;
      width: 3.6rem;
      height: 4rem;
      background-color: #fff;
      font-size: 0.3rem;
      padding: 0.47rem 0.41rem;
      p {
        line-height: 0.8rem;
      }
      .dialog-p1 {
        font-size: 0.36rem;
        color: #259bec;
        line-height: 0.5rem;
        margin-bottom: 0.3rem;
      }
    }
  }
}
</style>
<style lang="less">
.co-Page {
  overflow: auto;
}
</style>



