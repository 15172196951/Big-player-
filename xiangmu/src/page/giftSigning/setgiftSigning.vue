<template>
    <div class="setgiftSigning">
        <Head msg="签赠设置"/>
        <!-- 头部下拉 -->
        <!-- <div>{{orgId}}</div> -->
      <div class="select co-flex co-ac co-of" @click="selectStores">
          <p class="text-title co-te" :class="{'isclolor':!isShow}">{{curOrg}}</p>
            <x-icon class="fs-0"
                    type="ios-arrow-down" :class="{'isarrow':!isShow}"></x-icon>
            <x-icon type="ios-arrow-up" :class="{'isarrow':isShow}"></x-icon>   
        </div>
        <div class="giftAdd co-flex co-jsb" v-if="isShow">
            <p>签赠人管理</p>
            <p @click="giftAdd">
                <img src="../../assets/images/add1.png" alt="#">
                <span>新增签赠人</span>
            </p>
        </div>
        <scroll-list v-if="isShow"
                     :page-size="pageSize"
                     @show-data="showData"
                     pull-up-load
                     ref="scroll"
        >
              <div class="co-bg-0 co-flex contentbox1" @click="jumpDetail(item.guid,item.id,index)" v-for="(item,index) in DetailList" :key="index">
                  <img v-avatar="name"
                      class="round round-mg-06 fs-0" />
                  <div class="co-bd-b content co-of fg-1" style="padding-top:0.7rem;padding-bottom:0.25rem;padding-right:0.32rem">
                      <p class="content-name co-te">我叫小明</p>
                      <p  class="content-address">签赠限制><span>{{item.checkGiftTotal}}</span>币/月</p>
                  </div>
              </div>
        </scroll-list>
        <div class="bj-dialog" v-if="showDialog">
              <div class="dialog-content">
                  <p class="dialog-p1">编辑</p>
                  <p @click="xiugai">修改签赠人</p>
                  <p @click="detele">删除签赠人</p>
                  <p @click="quxiao">取消</p>
              </div>
          </div>
        <select-org v-if="!isShow" :selectvalue="curOrg" @selectd="getOrg" @selectshop="getSpell">
        </select-org>
    </div>
</template>
<script>
import Head from './heard.vue'
import ScrollList from '@c/ScrollList'
import SelectOrg from '@c/SelectOrg'
import { APIS } from '@a/js/config.js'
import { cookie } from 'vux'
export default {
  components: {
    Head,
    SelectOrg,
    ScrollList
  },
  data () {
    return {
      name: '小明',
      showDialog: false,
      isShow: true,
      curOrg: '',
      orgId: '', // 门店编码
      DetailList: [],
      pageIndex: 0,
      pageSize: 10,
      i: null,
      guid: '', // 点击的时候获取的员工guid
      id: '', // 测试传递到修改页面的签赠人名字
      shopCode: 'csxmd' // 测试修改店铺的Code
    }
  },
  created () {
    this.getInfo()
  },
  mounted () {
  },
  methods: {
    giftAdd () {
      this.$router.push({ path: '/giftSigning/new', query: { orgId: this.orgId } })
    },
    xiugai () {
      this.$router.push({ path: '/giftSigning/changstaff', query: { id: this.id, guid: this.guid, orgId: this.orgId } })
    },
    detele () {
      this.$axios({
        url: APIS.Deletegiftsigning,
        method: 'get',
        params: {guid: this.guid},
        headers: {'Content-Type': 'application/json;charset=UTF-8'}
      }).then(res => {
        if (res.data.status === '1') {
          this.showDialog = false
          this.DetailList.splice(this.i, 1)
        } else {
          this.$vux.toast.show({
            type: 'text',
            text: '删除失败'
          })
        }
      })
    },
    quxiao () {
      this.showDialog = false
    },
    jumpDetail (guid, id, index) {
      this.i = index
      this.showDialog = true
      this.guid = guid
      this.id = id
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
        this.showData({
          type: 0,
          cb: (len) => {
            this.$refs.scroll.upShow(len)
          }
        })
      })
    },
    getOrg (val) {
      console.log(val)
      this.curOrg = val.org_name
      this.orgId = val.org_code
      this.shopCode = 'NDT01'
      // this.getUpdate()
      this.showData({
        type: 0,
        cb: (len) => {
          this.$refs.scroll.upShow(len)
        }
      })
    },
    getSpell (obj, bool) {
      this.curOrg = obj.text
      this.orgId = obj.code
      this.shopCode = 'NDT01'
      this.showData({
        type: 0,
        cb: (len) => {
          this.$refs.scroll.upShow(len)
        }
      })
    },
    showData (obj) {
      console.log(obj.cb)
      if (obj.type === 0) {
        this.pageIndex = 0
      } else {
        console.log('执行else')
        this.pageIndex ++
      }
      this.$loading.loading('加载中')
      this.$axios({
        url: APIS.Setgiftsigning,
        method: 'get', // 两个shopCode NDT01 csxmd
        params: {shopCode: this.shopCode, pageIndex: this.pageIndex, pageSize: this.pageSize, givenType: 1},
        headers: {'Content-Type': 'application/json;charset=UTF-8'}
      }).then(res => {
        this.$loading.hideLoading()
        let result = res.data.result.result
        if (obj.type === 0) {
          this.DetailList = result
        } else {
          this.DetailList = this.DetailList.concat(result)
        }
        obj.cb(result.length, this.pageIndex, res.data.result.pageIndex)
      })
    },
    getUpdate () {
      this.$axios({
        url: APIS.Setgiftsigning,
        method: 'get', // 两个shopCode NDT01 csxmd
        params: {shopCode: this.shopCode, pageIndex: this.pageIndex, pageSize: this.pageSize, givenType: 1},
        headers: {'Content-Type': 'application/json;charset=UTF-8'}
      }).then(res => {
        this.DetailList = res.data.result.result
        let _self = this
        this.showData({
          type: 0,
          cb (len) {
            _self.$refs.scroll.upShow(len)
          }
        })
      })
    }
  }
}
</script>
<style lang="less" scoped>
.setgiftSigning {
  display: block;
  width: 100%;
  height: 100%;
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
        margin-right: 0.375rem;
        font-size: 0.7rem;
      }
      .text-title.isclolor {
        color: #259bec;
      }
    }
  .giftAdd {
    font-size: 0.75rem;
    padding: 0 0.75rem;
    height: 2.25rem;
    line-height: 2.25rem;
    img {
      vertical-align: top;
      width: 0.73rem;
      height: 0.73rem;
      margin-top: 0.73rem;
    }
  }
    .contentbox1 {
      margin-top: 0.05rem;
      margin-bottom: 0.05rem;
    }
    .round {
      border-radius: 100%;
      width: 1.8rem;
      height: 1.8rem;
    }
    .content-name {
      font-size: 0.7rem;
      color: #222222;
      line-height: 1rem;
      margin-bottom: 0.3rem;
    }
    .content-address {
      line-height: 0.93rem;
      font-size: 0.65rem;
      color: #888888;
    }
    .round-mg-06 {
      margin: 0.8rem 0.6rem 0.8rem 0.75rem;
    }
    .fs-0 {
      flex-shrink: 1; //缩小比例
    }
    .fg-1 {
      flex-grow: 1; //放大比例
    }
  
  .bj-dialog {
    position: fixed;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: #222222;
    background: rgba(0, 0, 0, 0.6);
    z-index: 1;
    .dialog-content {
      position: absolute;
      top: 13.28rem;
      left: 4.88rem;
      width: 9rem;
      height: 10rem;
      background-color: #fff;
      font-size: 0.75rem;
      padding: 1.18rem 1.03rem;
      p {
        line-height: 2rem;
      }
      .dialog-p1 {
        font-size: 0.9rem;
        color: #259bec;
        line-height: 1.25rem;
        margin-bottom: 0.75rem;
      }
    }
  }
}
</style>
<style lang="less">
.co-Page {
  overflow: auto;
}
.vux-search-box{
    top:8.5rem !important;
  }
  .wrapper {
  height: 84.4%;
}
</style>



