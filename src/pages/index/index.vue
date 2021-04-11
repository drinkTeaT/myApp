<template>
  <view>
    <AtTabBar
      fixed
      :tabList="tabList1"
      @click="onClick"
      :current="current1"
    />
  </view>
</template>
<script>
import {AtTabBar} from "taro-ui-vue3";
import './index.scss'
export default {
  name: 'TabBarPage',
  components:{AtTabBar},
  data() {
    return {
      current1: 1,
      tabList1: [
        { title: '待办事项', text: 8 },
        { title: '拍照' },
        { title: '通讯录', dot: true }
      ],
    }
  },
  methods: {
    onClick(value) {
      this.current1 = value
    }
  },
}
</script>
