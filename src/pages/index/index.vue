<template>
  <view>
    <AtTabBar fixed :current="current1" :tabList="tabList1" @click="onClick"/>
  </view>
</template>

<script>
import './index.scss'
import {AtTabBar} from 'taro-ui-vue3'
import Taro, {useState, useEffect} from "@tarojs/taro";

export default {
  components: {AtTabBar},
  data() {
    return {
      msg: '',
      current1: 0,
      tabList1: [],
    }
  },
  methods: {
    onClick(value) {
      // this.tabList1 = [{'title': 22}]
    }
  },
  created() {
    this.msg = 'gg'
    let params = {
      "nodeId": 1
    }
    Taro.request({url: 'http://localhost:8099/config/node/getTreeByNodeId', data: params},).then(res => {
      let result = res.data.data
      for (let child = 0; child < result.children.length; child++) {
        let obj = new Object()
        obj['title'] = result.children[child].label
        this.tabList1.push(obj)
      }
    })
  }
}
</script>
