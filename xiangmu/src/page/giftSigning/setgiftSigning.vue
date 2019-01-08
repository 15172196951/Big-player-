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
        <div class="content">
            <!-- 签赠人员展示 -->
            <!-- <div class="co-bg-0 co-flex" @click="jumpDetail()">
                <img v-avatar="name"
                    class="round round-mg-06 fs-0" />
                <div class="co-bd-b content co-of fg-1" style="padding-top:0.625rem;padding-bottom:0.625rem;padding-right:0.725rem">
                    <p class="content-name co-line-h1 co-te">我是新明</p>
                    <p  class="content-address">华南区/啥子/嗯嗯</p>
                </div>
            </div> -->
            <!-- 签赠人员编辑弹窗 -->
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
import Head from './heard.vue'
document.documentElement.style.fontSize = document.documentElement.clientWidth / 7.5 + 'px'
export default {
  components: {
    Head
  },
  data () {
    return {
        name:"小红",
        showDialog:true
    }
  },
  mounted () {},
  methods: {
      giftAdd(){
          this.$router.push({path:'/giftSigning/new'});
      },
      xiugai(){
          console.log("修改被电击")
      },
      detele(){
          console.log("删除被电击")
      },
      quxiao(){
          this.showDialog=false;
      }
  }
}
</script>
<style lang="less">
    .setgiftSigning{
        display: block;
        width: 100%;
        height: 100%;
        // background-color: aqua;
        .shopSelect{
            height: 0.9rem;
            font-size: 0.28rem;
            margin-bottom: 0.3rem;
            padding-left: 0.4rem;
            line-height:0.9rem;
        }
        .giftAdd{
            font-size: 0.3rem;
            padding: 0 0.3rem;
            height: 0.9rem;
            line-height: 0.9rem;
            img{
                vertical-align:top;
                width: 0.29rem;
                height: 0.29rem;
                margin-top: 0.29rem;
            }
        }
        .bj-dialog{
            position: absolute;
            top:0;
            width: 100%;
            height: 100%;
            background-color: #222222;
            background:rgba(0,0,0,0.6) ;
            z-index: 1;
            .dialog-content{
                position: absolute;
                top:5.31rem;
                left:1.95rem;
                width: 3.6rem;
                height: 4rem;
                background-color: #fff;
                font-size: 0.3rem;
                padding: 0.47rem 0.41rem;
                p{
                    line-height: 0.8rem;
                }
                .dialog-p1{
                    font-size: 0.36rem;
                    color: #259BEC;
                    line-height: 0.5rem;
                    margin-bottom: 0.3rem;
                }
            }
        }
    }
</style>


