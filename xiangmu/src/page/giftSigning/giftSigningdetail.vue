<template>
    <div class="giftSigningdetall">
        <Head msg="签赠明细"/>
        <div class="select">西安李家村万达店铺</div>
        <div class="Date">
            日历控件
        </div>
        <div class="content">
            <div class="top co-flex co-jsb">
                <p>
                    <img src="../../assets/images/my.png" alt="">
                    <span>张三</span>
                </p>
                <p>
                    <span>2018-11-23</span>
                    <span class="top-span">13:45</span>
                </p>
            </div>
            <div class="bottom">
                <p class="bottom-p1 co-flex co-jsb">
                    <span>WH9874734</span>
                    <span>100</span>
                </p>
                <p class="bottom-p2 co-flex co-jsb">
                    <span>客户赔币</span>
                    <span class="game">游戏币</span>
                </p>
            </div>
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
<style lang="less" scoped>
    .giftSigningdetall{
        display: block;
        width: 100%;
        height: 100%;
        .select {
            width: 100%;
            height: 0.9rem;
            font-size: 0.28rem;
            background-color: #fff;
            padding-left: 0.4rem;
            line-height: 0.9rem;
        }
        .Date{
            padding: 0 0.3rem;
            font-size: 0.3rem;
            height: 0.8rem;
        }
        .content{
            padding: 0 0.3rem;
            .top{
                font-size: 0.28rem;
                height: 0.8rem;
                line-height: 0.8rem;
                color: #888888;
                img{
                    width: 0.4rem;
                    height: 0.4rem;
                    vertical-align:top;
                    margin-top: 0.2rem;
                }
                .top-span{
                    margin-left: 0.05rem;
                }
            }
            .bottom{
                height: 1.36rem;
                padding: 0.22rem 0 0.2rem 0;
                .bottom-p1{
                    font-size: 0.3rem;
                    color: #222222;
                }
                .bottom-p2{
                    font-size: 0.26rem;
                    line-height: 0.6rem;
                    color: #888888;
                    .game{
                        color: #333333;
                    }
                }
            }
        }
    }
</style>
<style lang="less">
    .co-Page{
            position:relative ;
            }
</style>





