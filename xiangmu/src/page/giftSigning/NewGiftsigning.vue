<template>
    <div class="newGiftsigning">
        <Head msg="新建签赠人"/>
        <div class="Signperson co-flex co-jsb">
            <p>签赠人</p>
            <p @click="goYuangong">
                <img src="../../assets/images/rightjiantou.png" alt="#">
            </p>
        </div>
        <div class="everyDay">
            <x-input
                title="每月游戏币签赠上限"
                v-model="lengthP"
                text-align="right"  
                placeholder="请输入小于10000的整数"
                @on-change="aa"
                type=number
                :max=4
            ></x-input>
        </div>
        <div class="btnBox">
           <x-button type="primary" :disabled='disa' class="btn" @click.native="baocun">保存</x-button>
        </div>
    </div>
</template>
<script>
import Head from './heard.vue'
import { XInput, XButton } from 'vux'
import { APIS } from '@a/js/config.js'
export default {
  components: {
    Head,
    XInput,
    XButton
  },
  data () {
    return {
      lengthP: '',
      uuid: '',
      uuid1: ''
    }
  },
  computed: {
    disa () {
      if (this.lengthP !== '' && this.lengthP.length < 5) {
        return false
      } else {
        return true
      }
    }
  },
  mounted () {},
  methods: {
    goYuangong () {
      this.$router.push({ path: '/giftSigning/staff' })
    },
    aa () {
      console.log(this.lengthP)
    },
    baocun () {
      let time = this.getNewtime()
      let guid = this.$route.query.orgId // 获取设置页面传过来的店铺id 也就是这个页面的guid
      console.log(guid)
      this.uuid = this.getGuid()
      this.uuid1 = this.getGuid()
      // console.log('保存按钮被点击')
      // console.log(this.uuid)
      // console.log(this.uuid1)
      this.$axios({
        url: APIS.Addgiftsigning,
        method: 'get',
        params: {
          obj: {
            shopCode: 'csxmd', // 两个shopCode NDT01 csxmd
            jobCode: this.uuid,
            guid: this.uuid1,
            createTime: time,
            giveTotalCount: this.lengthP
          }
        },
        headers: { 'Content-Type': 'application/json;charset=UTF-8' }
      }).then(res => {
        if (res.data.status === '1') {
          this.$vux.toast.show({
            type: 'text',
            text: '添加签赠人成功'
          })
        } else {
          this.$vux.toast.show({
            type: 'text',
            text: '添加签赠人失败'
          })
        }
      })
    },
    // 随机获取guid
    getGuid () {
      var s = []
      var hexDigits = '0123456789abcdef'
      for (var i = 0; i < 36; i++) {
        s[i] = hexDigits.substr(Math.floor(Math.random() * 0x10), 1)
      }
      s[14] = '4'
      s[19] = hexDigits.substr((s[19] & 0x3) | 0x8, 1)
      s[8] = s[13] = s[18] = s[23] = '-'

      var uuid = s.join('')
      return uuid
    },
    // 获取点击签赠时候的当前时间
    getNewtime () {
      let date = new Date()
      let seperator1 = '-'
      let seperator2 = ':'
      let month = date.getMonth() + 1
      let strDate = date.getDate()
      if (month >= 1 && month <= 9) {
        month = '0' + month
      }
      if (strDate >= 0 && strDate <= 9) {
        strDate = '0' + strDate
      }
      let currentdate = date.getFullYear() + seperator1 + month + seperator1 + strDate + ' ' + date.getHours() + seperator2 + date.getMinutes() + seperator2 + date.getSeconds()
      return currentdate
    }
  }
}
</script>
<style lang="less" scoped>
.newGiftsigning {
  display: block;
  width: 100%;
  height: 100%;
  .Signperson {
    height: 2.25rem;
    line-height: 2.25rem;
    font-size: 0.75rem;
    padding: 0 0.75rem;
    img {
      width: 0.8rem;
      height: 0.8rem;
      margin-top: 0.73rem;
    }
  }
  .everyDay {
    height: 2.25rem;
    line-height: 2.25rem;
    font-size: 0.75rem;
    margin-bottom: 21.85rem;
  }
  .btnBox {
    padding: 0 0.75rem;
    text-align: center;
    .weui-btn_disabled.weui-btn_primary {
        background-color: #dcdcdc;
      }
    .btn {
      border: 0;
      background-color: none;
      width: 16.75rem;
      height: 2rem;
      background-color: #259bec;
      color: #fff;
      font-size: 0.8rem;
      border-radius: 0.2rem;
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
  padding: 0 0.75rem !important;
}
.weui-label {
  width: 100% !important;
}
</style>


