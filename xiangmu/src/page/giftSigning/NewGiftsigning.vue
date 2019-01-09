<template>
    <div class="newGiftsigning">
        <Head msg="新建签赠人"/>
        <div class="Signperson co-flex co-jsb">
            <p>签赠人</p>
            <p @click="goYuangong">
                <img src="../../assets/images/rightjiantou.png" alt="">
            </p>
        </div>
        <div class="everyDay">
            <x-input
                title="每月游戏币签赠上限"
                v-model="lengthP"
                text-align="right"  
                placeholder="未输入"
                @on-change="aa"
            ></x-input>
        </div>
        <div class="btnBox">
           <button class="btn" @click="baocun">保存</button>
        </div>
    </div>
</template>
<script>
import Head from "./heard.vue";
import { XInput } from "vux";
document.documentElement.style.fontSize =
  document.documentElement.clientWidth / 7.5 + "px";
export default {
  components: {
    Head,
    XInput
  },
  data() {
    return {
      lengthP: ""
    };
  },
  mounted() {},
  methods: {
    goYuangong() {
      this.$router.push({ path: "/giftSigning/staff" });
    },
    aa() {
      console.log(this.lengthP);
    },
    baocun() {
      console.log("保存按钮被点击");
    }
  }
};
</script>
<style lang="less" scoped>
.newGiftsigning {
  display: block;
  width: 100%;
  height: 100%;
  .Signperson {
    height: 0.9rem;
    line-height: 0.9rem;
    font-size: 0.3rem;
    padding: 0 0.3rem;
    img {
      width: 0.32rem;
      height: 0.32rem;
      margin-top: 0.29rem;
    }
  }
  .everyDay {
    height: 0.9rem;
    line-height: 0.9rem;
    font-size: 0.3rem;
    margin-bottom: 8.74rem;
  }
  .btnBox {
    padding: 0 0.3rem;
    text-align: center;
    .btn {
      border: 0;
      background-color: none;
      width: 6.7rem;
      height: 0.8rem;
      background-color: #259bec;
      color: #fff;
      font-size: 0.32rem;
      border-radius: 0.08rem;
    }
  }
}
</style>
<style lang="less">
input::-webkit-input-placeholder {
  color: #aaaaaa;
}
input::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: #aaaaaa;
}
input:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: #aaaaaa;
}
input:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: #aaaaaa;
}
.weui-cell {
  padding: 0 0.3rem !important;
}
.weui-label {
  width: 100% !important;
}
</style>


