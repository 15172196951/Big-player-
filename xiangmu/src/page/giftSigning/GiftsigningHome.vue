<template>
  <div class="giftSigning">
    <div class="box">
    <Head msg="签赠"/>
    <div class="select">西安李家村万达店铺</div>
    <div class="giftcontent">
      <div class="membernum">
        <span>会员卡号</span>
        <input type="text" placeholder="请输入会员名" style='color:#222222;font-size:0.32rem' v-model="giftcontent.memberName">
        <img src="../../assets/images/saoyisao.png" alt="#" @click="saoyisao">
      </div>
      <div class="sign-content co-flex co-jsb">
        <span>签赠内容</span>
        <checker default-item-class="demo5-ite" selected-item-class="demo5-item-selected">
          <checker-item :value="1" @on-item-click="getValue" v-model="giftcontent.gameCurrency">游戏币</checker-item>
        </checker>
        <checker default-item-class="demo5-ite1" selected-item-class="demo5-item-selected2">
          <checker-item :value="2">游戏券</checker-item>
        </checker>
        <span></span>
        <span></span>
      </div>
      <div class="giftnum">
        <span>签赠数量</span>
        <input type="text" placeholder="请输入数量" style='color:#F98125;font-size:0.6rem' @input="handleInput" :value="val" />
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
      <x-button type="primary" :disabled="btnDisable" class="btn" @click.native="queren">确认</x-button>
    </div>
    <div class="gift-foot co-flex co-jsb">
      <div class="foot-left">
        <img src="../../assets/images/set.png" alt="#">
        <router-link :to="{name:'setgiftSigning'}">签赠设置</router-link>
      </div>
      <div class="foot-right">
        <img src="../../assets/images/mingxi.png" alt>
        <router-link :to="{name:'giftSigningdetall'}">签赠明细</router-link>
      </div>
    </div>
    <div v-if="showDialog" class="dialog">
      <div class="dialog-content">
          <ul class="dialog-ul">
            <li>
                <span class="dialog-title">签赠会员：</span>
                <span>{{giftcontent.memberName}}</span>
            </li>
            <li>
                <span class="dialog-title">签赠内容：</span>
                <span>{{giftcontent.gameCurrency}}</span>
            </li>
            <li>
                <span class="dialog-title">签赠数量：</span>
                <span class="dialog-num">{{val}}</span>
            </li>
          </ul>
          <div class="dialog-btn co-flex co-flex co-jsb">
            <span @click="dialogNo">取消</span>
            <span class="dialog-querenBtn" @click="dialogYes">确认签赠</span>
          </div>
      </div>
    </div>
  </div>
  </div>
</template>
<script>
import Head from "./heard.vue";
import { Checker, CheckerItem, XButton, Group, Selector, XInput } from "vux";
document.documentElement.style.fontSize =
  document.documentElement.clientWidth / 7.5 + "px";
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
  data() {
    return {
      demo5: 1,
      demo01: "",
      list: [
        { key: "gd", value: "接待用币" },
        { key: "gx", value: "赔赠用币" }
      ],
      lengthP: "",
      val: null,
      giftcontent: {
        memberName: null,
        gameCurrency: "游戏币"
      },
      showDialog: false
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
      console.log("确认按钮被点击");
      console.log(this.giftcontent.memberName);
      console.log(this.val);
      this.showDialog = true;
    },
    aa() {
      if (this.lengthP.length >= 10) {
        // console.log(`1`);
        this.lengthP = this.lengthP.substring(0, 10) + "...";
      } else {
        console.log(`2`);
      }
    },
    saoyisao() {
      console.log("扫一扫被电击");
    },
    handleInput(e) {
      this.val = e.target.value.replace(/[^\d]/g, "");
    },
    dialogYes() {
      console.log("确认签赠被电击");
    },
    dialogNo() {
      this.showDialog = false;
    }
  }
};
</script>
<style lang="less" scoped>
.giftSigning {
  // background-color: #aaaaaa;
  .box {
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
        padding-right: 0.3rem;
        input::-webkit-input-placeholder {
          color: #aaaaaa;
          font-size: 0.32rem;
        }
        span {
          float: left;
          margin-right: 0.6rem;
        }
        input {
          line-height: 1.3rem;
          float: left;
          background: none;
          outline: none;
          border: 0;
          margin-right: 0.5rem;
        }
        img {
          float: left;
          margin-top: 0.41rem;
          width: 0.48rem;
          height: 0.48rem;
          vertical-align: top;
        }
      }
      .sign-content {
        height: 1.3rem;
        line-height: 1.3rem;
        .demo5-ite,
        .demo5-ite1 {
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
          background: url("../../assets/images/active.png") no-repeat right
            bottom;
          background-size: 0.36rem 0.36rem;
          color: #259bec;
          border: 1px solid #259bec;
          border-radius: 0.04rem;
        }
      }
      .giftnum {
        height: 1.3rem;
        line-height: 1.3rem;
        span {
          float: left;
          margin-right: 0.6rem;
        }
        input::-webkit-input-placeholder {
          color: #aaaaaa;
          font-size: 0.32rem;
        }
        input {
          line-height: 1.1rem;
          width: 50%;
          float: left;
          background: none;
          outline: none;
          border: 0;
        }
      }
    }
    .yongtu {
      height: 1.8rem;
      font-size: 0.3rem;
      background-color: #fff;
      margin-bottom: 0.6rem;
      padding-right: 0.2rem;
    }
    .btnbox {
      margin-bottom: 2.62rem;
      .weui-btn_disabled.weui-btn_primary {
        background-color: #dcdcdc;
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
    .dialog {
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: #222222;
      background: rgba(0, 0, 0, 0.6);
      z-index: 1;
      .dialog-content {
        padding: 0.66rem 0.92rem 0.29rem 0.92rem;
        top: 4.83rem;
        left: 1.05rem;
        width: 5.4rem;
        height: 3.72rem;
        font-size: 0.32rem;
        background-color: #fff;
        border-radius: 0.12rem;
        .dialog-ul {
          height: 1.68rem;
          margin-bottom: 0.64rem;
          li {
            overflow: hidden;
            height: 0.56rem;
            line-height: 0.56rem;
            span {
              color: #222222;
            }
            .dialog-num {
              color: #f98125;
            }
            .dialog-title {
              color: #888;
              font-size: 0.3rem;
            }
          }
        }
        .dialog-querenBtn {
          color: #259bec;
        }
      }
    }
  }
}
</style>
<style lang="less">
.weui-label {
  font-size: 0.3rem;
}
.weui-select {
  font-size: 0.3rem !important;
}
.weui-input {
  font-size: 0.3rem !important;
}
</style>