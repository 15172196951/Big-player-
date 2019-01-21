<template>
    <div class="giftSigningdetall">
      <div class="abcd">
        <Head msg="签赠明细"/>
        <!-- 头部下拉 -->
        <div class="select co-flex co-ac co-of" @click="selectStores">
          <p class="text-title co-te" :class="{'isclolor':!isShow}">{{curOrg}}</p>
            <x-icon class="fs-0"
                    type="ios-arrow-down" :class="{'isarrow':!isShow}"></x-icon>
            <x-icon type="ios-arrow-up" :class="{'isarrow':isShow}"></x-icon>   
        </div>
        <div class="Date" v-if="isShow">
          <div class="Date-show co-flex co-jsb" @click="DateShow">
              <span>{{value1}}</span>
              <img src="../../assets/images/date.png" alt="#">
          </div>
          <group v-show="false">
              <datetime  format="YYYY-MM" v-model="value1" :show="showDate" @on-change="DateChange" @on-cancel="DateCancel" @on-confirm="SetTime">
              </datetime>
          </group>
        </div>
        <scroll-list v-if="isShow"
                     :page-size="pageSize"
                     @show-data="showData1"
                     pull-up-load
                     ref="scroll"
        >
          <div class="content1" v-for="(item,index) in DetailList" :key="index">
              <div class="top co-flex co-jsb">
                  <p>
                      <img src="../../assets/images/my.png" alt="">
                      <span>张三</span>
                  </p>
                  <p>
                      <span class="top-span">{{item.currentDate}}</span>
                  </p>
              </div>
              <div class="bottom">
                  <p class="bottom-p1 co-flex co-jsb">
                      <span>{{item.cardNO}}</span>
                      <span>{{item.id}}</span>
                  </p>
                  <p class="bottom-p2 co-flex co-jsb">
                      <span>客户赔币</span>
                      <span class="game">游戏币</span>
                  </p>
              </div>
          </div>
          <div v-if="showError" style="text-align:center;margin-top:2rem;color:#555555;font-size:0.6rem;">{{error}}</div>
        </scroll-list>
        <select-org v-if="!isShow" :selectvalue="curOrg" @selectd="getOrg" @selectshop="getSpell">
        </select-org>
      </div>
      
    </div>
</template>
<script>
import Head from './heard.vue'
import { Datetime, Group, cookie } from 'vux'
import SelectOrg from '@c/SelectOrg'
import { APIS } from '@a/js/config.js'
import ScrollList from '@c/ScrollList'
export default {
  components: {
    Head,
    Datetime,
    Group,
    SelectOrg,
    ScrollList
  },
  data () {
    return {
      value1: '',
      showDate: false,
      isShow: true,
      curOrg: '', // 门店name
      orgId: '',  // 门店id 目前只有NDT01有数据返回
      pageSize: 10,
      pageIndex: 0,
      DetailList: [],
      error: '',
      showError: false,
      shopCode: 'NDT01'
    }
  },
  created () {
    this.nowDate()
    this.getInfo()
  },
  methods: {
    SetTime () {
      let _self = this
      this.shopCode = 'csxmd'
      this.showData1({
          type: 0,
          cb (len) {
            _self.$refs.scroll.upShow(len)
          }
        })

    },
    DateShow () {
      this.showDate = true
    },
    DateChange () {
      this.showDate = false
    },
    DateCancel () {
      this.showDate = false
    },
    nowDate () {
      let now = new Date()
      let yy = now.getFullYear() // 年
      let mm = now.getMonth() + 1 // 月
      let clock = yy + '-'
      if (mm < 10) clock += '0'
      clock += mm
      this.value1 = clock
    },
    selectStores () {
      if (this.isShow) {
        this.isShow = false
      } else {
        this.isShow = true
      }
    },
     // 初始化
    getInfo () {
      let _self = this
      this.$loading.loading('加载中')
      this.$axios({
        url: APIS.memberOrganization,
        method: 'get',
        params: { employee_id: cookie.get('creatorId'), org_guid: '' },
        headers: { 'Content-Type': 'application/json;charset=UTF-8' }
      }).then(res => {
        this.$loading.hideLoading()
        this.curOrg = res.data.result[0].org_name
        this.orgId = res.data.result[0].org_code
        this.showData1({
          type: 0,
          cb (len) {
            _self.$refs.scroll.upShow(len)
          }
        })
      })
    },
    getOrg (val, bool) {
      this.curOrg = val.org_name
      // this.orgId = val.org_code // 数据回来后取消注释，当切换店铺时更换orgId
      this.isShow = !bool
      this.shopCode = 'csxmd'
      this.showData1({
        type: 0,
        cb: (len) => {
          this.$refs.scroll.upShow(len)
        }
      })
    },
    getSpell (obj, bool) {
      this.curOrg = obj.text
      // this.orgId = obj.code // 数据回来后取消注释，当切换店铺时更换orgId
      this.shopCode = 'csxmd'
      this.isShow = !bool
      this.showData1({
        type: 0,
        cb: (len) => {
          this.$refs.scroll.upShow(len)
        }
      })
    },
    // 下拉刷新上拉加载
    showData1 (obj) {
      if (obj.type === 0) {
        this.pageIndex = 1
      } else {
        this.pageIndex ++
      }
      this.$loading.loading('加载中')
      this.$axios({
        url: APIS.giftsigningDetail,
        method: 'get',
        params: {shopCode: this.shopCode, time: this.value1, offset: this.pageIndex, limit: this.pageSize},
        headers: {'Content-Type': 'application/json;charset=UTF-8'}
      }).then(res => {
        this.$loading.hideLoading()
        if (res.data.status === 200) {
          let result = res.data.data.cashierGivenCoinDetaiList
          if (obj.type === 0) {
            this.DetailList = result
          } else {
            this.DetailList = this.DetailList.concat(result)
          }
          obj.cb(result.length, this.pageIndex)
        } else {
          this.showError = true
          this.error = res.data.error
          this.$vux.toast.show({
            type: 'text',
            text: '暂无数据'
          })
        }
      })
    },
  }
}
</script>
<style lang="less" scoped>
.giftSigningdetall {
  .abcd{
    width: 100%;
  .select {
      width: 100%;
      height: 2.25rem;
      margin-bottom: 0.75rem;
      font-size: 0.7rem;
      background-color: #fff;
      padding-left: 1rem;
      line-height: 2.25rem;
      .vux-x-icon {
        fill: #222222;
        width: 0.75rem;
        height: 0.75rem;
      }
      .isarrow {
        display: none;
      }
      .vux-x-icon-ios-arrow-up {
        fill: #259bec;
      }
      .text-title {
        margin-right: 0.38rem;
        font-size: 0.7rem;
      }
      .text-title.isclolor {
        color: #259bec;
      }
    }
  .Date {
    padding: 0 0.75rem;
    font-size: 0.75rem;
    height: 2rem;
    line-height: 2rem;
    color: #555555;
    font-size: 0.75rem;
    .Date-show {
      img {
        width: 1.05rem;
        height: 0.95rem;
        margin-top: 0.53rem;
      }
    }
  }
  .top {
    padding: 0 0.75rem;
    font-size: 0.7rem;
    height: 2rem;
    line-height: 2rem;
    color: #888888;
    img {
      width: 1rem;
      height: 1rem;
      vertical-align: top;
      margin-top: 0.5rem;
    }
    .top-span {
      margin-left: 0.13rem;
    }
  }
  .bottom {
    height: 3.4rem;
    padding: 0.55rem 0.75rem 0.5rem 0.75rem;
    .bottom-p1 {
      font-size: 0.75rem;
      color: #222222;
    }
    .bottom-p2 {
      font-size: 0.65rem;
      line-height: 1.5rem;
      color: #888888;
      .game {
        color: #333333;
      }
    }
  }
  
}
}
</style>
<style lang="less">
.weui-cell_access {
  padding-left: 0.75rem !important;
  color: #555555 !important;
  text-decoration: none;
  font-size: 0.75rem;
}
.weui-cell_access .weui-cell__ft:after {
  border-color: red !important;
  border-width: 0rem !important;
}
.vux-search-box{
  top:8.5rem !important;
}
.wrapper{
  height: 87.3%;
}
</style>





