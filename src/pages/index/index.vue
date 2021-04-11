<template>
  <view>
    <AtTabs
      :swipeable="false"
      :current="atTabCurrent"
      :tabList="tabDataList"
      @click="clickTab"
    >
      <AtTabsPane :current="atTabCurrent" v-for="(component,index) in componentData" :index="atTabCurrent" :key="index">
        <view class='tab-content'>
          <view v-for="(item,index) in component.children" :key="index">
            <!--开始遍历组件类型-->
          </view>
        </view>
      </AtTabsPane>
    </AtTabs>
  </view>
  <view>
    <AtTabBar
      fixed
      :tabList="tabBarData"
      @click="clickTabBar"
      :current=0
    />
  </view>
</template>

<script>
import './index.scss'
import Taro from "@tarojs/taro";
import {AtTabBar, AtTabs, AtTabsPane} from "taro-ui-vue3";

export default {
  components: {AtTabBar, AtTabs, AtTabsPane},
  data() {
    return {
      tabDataList: [],
      componentData: [],
      tabBarData: [
        {title: '首页', iconType: 'home'},
        {title: '搜索', iconType: 'search'},
        {title: '设置', iconType: 'settings'}
      ],
      atTabCurrent: 0
    }
  },
  methods: {
    clickTab(current) {
      this.atTabCurrent = current
    },
    clickTabBar(value) {
      // 切换yemia
    },
    initPage() {
      const self = this
      let params = {
        "nodeId": 23
      }
      Taro.request({url: 'http://localhost:8099/config/node/getTreeByNodeId', data: params},).then(res => {
        let result = res.data.data.children[0]
        self.componentData = result.children
        // 设置初始值
        for (let i = 0; i < self.componentData.length; i++) {
          let obj = new Object()
          obj['title'] = self.componentData[i].label
          self.tabDataList.push(obj)
        }
      })
    }
  },
  created() {
    this.initPage()
  }
}
</script>
