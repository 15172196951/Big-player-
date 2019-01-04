<template>
    <div class="giftSigning">
        <Head msg="签赠"/>
        <div class="select">
            西安李家村万达店铺
        </div>
        <div class="giftcontent">
            <div class="membernum co-flex co-jsb">
                <span>会员卡号</span>
                <input type="text" placeholder="请输入会员名">
                <img src="" alt="">
            </div>
            <div class="sign-content co-flex co-jsb">
                <span>签赠内容</span>
                <checker
                default-item-class="demo5-ite"
                selected-item-class="demo5-item-selected"
                >
                <checker-item :value="1" @on-item-click="getValue">游戏币</checker-item>
                </checker>
                <checker
                default-item-class="demo5-ite1"
                selected-item-class="demo5-item-selected2"
                >
                <checker-item :value="2">游戏券</checker-item>
                </checker>
            </div>
            <div class="giftnum co-flex co-jsb">
                <span>签赠数量</span>
                <span>100</span>
            </div>
        </div>
        <div class="yongtu">
            用途
        </div>
        <div class="beizhu">
            <span>
                备注
            </span>
            <span>大客户回馈招待，超出字符后面...</span>
        </div>
        <div class="btnbox">
            <x-button type="primary" class="btn" @click.native="queren">确认</x-button>
        </div>
        <div class="gift-foot co-flex co-jsb">
            <div class="foot-left">
                    <img src="../../assets/images/set.png" alt="">
                    <router-link :to="{name:'setgiftSigning'}">签赠设置</router-link>
            </div>
            <div class="foot-right">
                    <img src="../../assets/images/mingxi.png" alt="">
                    <router-link :to="{name:'giftSigningdetall'}">签赠明细</router-link>
            </div>
        </div>
    </div>
</template>
<script>
import Head from './heard.vue'
import { Checker, CheckerItem, XButton } from 'vux'
export default {
  components: {
    Head,
    Checker,
    CheckerItem,
    XButton
  },
  data () {
    return {
      demo5: 1
    }
  },
  mounted () {},
  methods: {
    getValue () {
      console.log(6666)
    },
    queren () {
      console.log('确认按钮被点击')
    }
  }
}
</script>
<style lang="less" scoped>
.giftSigning {
  display: block;
  width: 100%;
  a{
      text-decoration:none; 
  }
  .select {
    width: 100%;
    height: 2.25rem;
    margin-bottom: 0.75rem;
  }
  .giftcontent {
    height: 9.75rem;
    padding: 0.95rem 0.75rem;
    margin-bottom: 0.35rem;
    font-size: 0.8rem;
    .sign-content {
      .demo5-ite {
        color: #888888;
        width: 4.25rem;
        height: 1.5rem;
        border: 1px solid #D2D2D2;
        font-size: 0.7rem;
        line-height: 1.5rem;
        text-align: center;
      }
      .demo5-item-selected {
        color: #259bec;
        border: 1px solid #259bec;
      }
    }
  }
  .yongtu{
      height: 2.25rem;
      font-size: 0.75rem;
      line-height: 2.25rem;
      padding: 0 0.75rem;
  }
  .beizhu{
      height: 2.25rem;
      font-size: 0.75rem;
      line-height: 2.25rem;
      margin-bottom: 1.9rem;
      padding: 0 0.75rem;
  }
  .btnbox{
    margin-bottom: 6.55rem;
    .btn{
     width: 16.75rem;
     height: 2rem;
    }
  }
  .gift-foot{
     padding: 0 0.75rem;
     height: 1.05rem;
     line-height: 1.05rem;
      img{
        width: 0.88rem;
        height: 0.88rem;
         }
      a{
        color: #5A7C9A;
        font-size: 0.75rem; 
         }
     .foot-left{
         a{
             line-height: 1.05rem;
         }
        
     }
  }
}
 
</style>
<style lang="less">
</style>
