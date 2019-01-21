<template>
    <div class="ChangStaff">
        <Head msg="修改签赠人"/>
        <div class="Signperson co-flex co-jsb">
            <span>签赠人</span>
            <span>{{name}}</span>
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
           <x-button type="primary" :disabled='disa' class="btn" @click.native="bianji">编辑</x-button>
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
      shopCode: '',
      name: ''
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
  created () {
    this.getData()
  },
  methods: {
    bianji () {
      let guid = this.$route.query.guid
      console.log('编辑被点击')
      this.$axios({
        url: APIS.Updategiftsigning,
        method: 'get',
        params: {
          obj: {
            shopCode: 'csxmd', // 目前的服务只支持这个
            guid: guid,
            giveTotalCount: this.lengthP
          }
        },
        headers: {'Content-Type': 'application/json;charset=UTF-8'}
      }).then(res => {
        console.log(res.data.status)
        if (res.data.status === '1') {
          this.$vux.toast.show({
            type: 'text',
            text: '修改成功'
          })
        } else {
          this.$vux.toast.show({
            type: 'text',
            text: '修改失败'
          })
        }
      })
    },
    aa () {
      console.log(this.lengthP)
    },
    getData () {
      this.shopCode = this.$route.query.orgId
      this.name = this.$route.query.id
    }
  }
}
</script>

<style lang="less" scoped>
.ChangStaff{
    width: 100%;
    height: 100%;
    display: block;
    .Signperson{
        height: 2.25rem;
        padding: 0 0.75rem;
        line-height: 2.25rem;
        font-size: 0.75rem;
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


