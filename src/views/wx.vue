<template>
  <div class="page">
    <div class="wrap">
      <p>需要用户触发的，不必放在wx.ready()方法中;</p>
      <p>
        若需要页面加载时就执行的话，如分享接口，就必须放在wx.ready()方法中执行
      </p>
      <p>sohu获取用户ip：</p>
      <van-divider>{{returnCitySN}}</van-divider>
      <p>wx开发作者工具查看：</p>
      <van-button type="primary" @click="getNetworkType()">网络状态</van-button>
      <van-button type="primary" @click="getLocation()">地理位置</van-button>
      <van-divider>{{ networkType }}</van-divider>
      <van-divider>lng: {{ longitude }}, lat: {{ latitude }}</van-divider>
    </div>
  </div>
</template>

<script>
// js 引入的 无法提到公共
import { Dialog, Toast } from 'vant';
export default {
  mixins: [],
  components: {},
  props: {},
  data() {
    return {
      returnCitySN: window.returnCitySN,
      networkType: '',
      longitude: '',
      latitude: ''
    };
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  destroyed() {},
  methods: {
    getNetworkType() {
      let _that = this
      wx.getNetworkType({
        success: function(res) {
          Toast(res)
          _that.networkType = res.networkType // 返回网络类型2g，3g，4g，wifi
        }
      });
    },
    getLocation() {
      let _that = this
      wx.getLocation({
        success: function(res) {
          Toast(res)
          _that.longitude = res.longitude
          _that.latitude = res.latitude
        },
        cancel: function(res) {
          console.log('用户拒绝授权获取地理位置')
        }
      })
    }
  }
}
</script>

<style scoped lang="less">
.page {
  position: relative;
  width: 100%;
  height: 100%;
  background: #fafafa; //灰色
  font-size: 14px;
  text-align: left;
  vertical-align: middle;
  word-wrap: break-word;
  .wrap {
    background-color: #ffffff;
    height: 100%;
    padding: 0 15px;
    p {
      text-align: left;
    }
    button {
      margin: 0 20px;
    }
  }
}
</style>
