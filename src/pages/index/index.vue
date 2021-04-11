<template>
  <view>
    <AtTabBar
      :tabList="[
        {title: '首页', iconType: 'home'},
        {title: '搜索', iconType: 'search'},
        {title: '设置', iconType: 'settings'}
      ]"
      @click="clickTabBar"
      :current=1
    />
  </view>
</template>

<script>
import './index.scss'
import Taro from "@tarojs/taro";
import {AtTabBar} from "taro-ui-vue3";

export default {
  name: 'TabBarPage',
  components: {AtTabBar},
  data() {
    return {
      componentData: [],
      tabBarData: [
        {title: '首页', iconType: 'home'},
        {title: '搜索', iconType: 'search'},
        {title: '设置', iconType: 'settings'}
      ],
    }
  },
  methods: {
    clickTabBar(value) {
      // this.tabList1 = [{'title': 22}]
    },
    initPage() {
      let params = {
        "nodeId": 23
      }
      Taro.request({url: 'http://localhost:8099/config/node/getTreeByNodeId', data: params},).then(res => {
        let result = res.data.data.children[0]
        this.componentData = result
        // 初始化数据
      })
    }
  },
  created() {
    this.initPage()
  }
}
</script>
