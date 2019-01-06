<template>
  <div class="giftSigning">
    <Head msg="签赠"/>
    <div class="select">西安李家村万达店铺</div>
    <div class="giftcontent">
      <div class="membernum co-flex co-jsb">
        <span>会员卡号</span>
        <input type="text" placeholder="请输入会员名">
        <img src alt>
      </div>
      <div class="sign-content co-flex co-jsb">
        <span>签赠内容</span>
        <checker default-item-class="demo5-ite" selected-item-class="demo5-item-selected">
          <checker-item :value="1" @on-item-click="getValue">游戏币</checker-item>
        </checker>
        <checker default-item-class="demo5-ite1" selected-item-class="demo5-item-selected2">
          <checker-item :value="2">游戏券</checker-item>
        </checker>
      </div>
      <div class="giftnum co-flex co-jsb">
        <span>签赠数量</span>
        <span>100</span>
      </div>
    </div>
    <div class="yongtu">
      <group label-width="4.5em" label-margin-right="2em" label-align="left">
        <selector v-model="demo01" title="用途" :options="list" direction="rtl"></selector>
        <x-input
          title="备注"
          v-model="lengthP"
          text-align="right"
          placeholder="请输入备注"
          @on-change="aa"
        ></x-input>
      </group>  
    </div>
    <div class="btnbox">
      <x-button type="primary" :disabled="btnDisable" class="btn" @click.native="queren" @button-primary-disabled-bg-color="">确认</x-button>
    </div>
    <div class="gift-foot co-flex co-jsb">
      <div class="foot-left">
        <img src="../../assets/images/set.png" alt>
        <router-link :to="{name:'setgiftSigning'}">签赠设置</router-link>
      </div>
      <div class="foot-right">
        <img src="../../assets/images/mingxi.png" alt>
        <router-link :to="{name:'giftSigningdetall'}">签赠明细</router-link>
      </div>
    </div>
  </div>
</template>
<script>
import Head from './heard.vue'
import { Checker, CheckerItem, XButton, Group, Selector, XInput } from 'vux'
document.documentElement.style.fontSize =
  document.documentElement.clientWidth / 7.5 + 'px'
export default {
  components: {
    Head,
    Checker,
    CheckerItem,
    XButton,
    Group,
    Selector,
    XInput
  },
  data () {
    return {
      demo5: 1,
      demo01: "",
      list: [{ key: "gd", value: "招待用币" }, { key: "gx", value: "游戏币" }],
      lengthP: ""
    };
  },
  computed: {
    btnDisable() {
      if (this.demo01 != "") {
        console.log(1111);
        return false;
      } else {
        console.log(222);
        return true;
      }
    }
  },
  methods: {
    getValue() {
      console.log(6666);
    },
    queren() {
      console.log('确认按钮被点击');
    },
    aa() {
      if (this.lengthP.length >= 10) {
        // console.log(`1`);
        this.lengthP = this.lengthP.substring(0, 10) + "...";
      } else {
        console.log(`2`);
      }
    }
  },
  
};
</script>
<style lang="less" scoped>
.giftSigning {
  display: block;
  width: 100%;
  a {
    text-decoration: none;
  }
  .select {
    width: 100%;
    height: 0.9rem;
    margin-bottom: 0.3rem;
    font-size: 0.28rem;
    background-color: #fff;
    padding-left: 0.4rem;
    line-height: 0.9rem;
  }
  .giftcontent {
    height: 3.9rem;
    font-size: 0.32rem;
    margin-bottom: 0.3rem;
    background-color: #fff;
    padding-left: 0.3rem;
    .membernum {
      height: 1.3rem;
      line-height: 1.3rem;
    }
    .sign-content {
      height: 1.3rem;
      line-height: 1.3rem;
      .demo5-ite {
        color: #888888;
        width: 1.7rem;
        height: 0.6rem;
        border: 0.02rem solid #d2d2d2;
        font-size: 0.28rem;
        line-height: 0.6rem;
        text-align: center;
        border-radius: 0.04rem;
      }
      .demo5-item-selected {
        color: #259bec;
        border: 1px solid #259bec;
      }
    }
    .giftnum {
      height: 1.3rem;
      line-height: 1.3rem;
    }
  }
  .yongtu {
    height: 1.8rem;
    font-size: 0.3rem;
    background-color: #fff;
    margin-bottom: 0.6rem;
  }
  .btnbox {
    margin-bottom: 2.62rem;
    .weui-btn_disabled.weui-btn_primary{
      background-color:#DCDCDC;
    }
    .btn {
      width: 6.7rem;
      height: 0.8rem;
    }
  }
  .gift-foot {
    padding: 0 0.3rem;
    height: 0.42rem;
    line-height: 0.2rem;
    img {
      width: 0.351rem;
      height: 0.351rem;
      vertical-align: top;
      line-height: 0.42rem;
      margin-top: 0.035rem;
    }
    a {
      color: #5a7c9a;
      font-size: 0.3rem;
    }
  }
}
</style>
<style lang="less">
</style>
