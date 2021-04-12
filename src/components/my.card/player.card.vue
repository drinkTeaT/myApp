<template>
  <view style="display: flex;justify-content: center;font-size: 16px">{{leafConfigData.title}}</view>
  <view class="flex-wrp flex-wrp-row">
    <view v-for="(card, index) in  cardData" :key="index">
      <AtCard
        class="flex-item"
        style="margin-left: 0px;margin-right: 0px;"
        :note='card.note'
        :extra='card.extra'
        :title='card.title'
      >
        <view style="display: flex;justify-content: center">
          <image :style="cardStyle()" :model="heightFix" :src=card.imgSrc></image>
        </view>
      </AtCard>
    </view>
  </view>
</template>

<script>
import './player.card.scss'
import {AtCard} from 'taro-ui-vue3'
import Taro from "@tarojs/taro";

export default {
  name: "MyCard",
  components: {AtCard},
  props: {
    item: null,
    leafDataMap: null
  },
  data() {
    return {
      cardData: [],
      leafConfigData: null,
    }
  },
  methods: {
    dataToObject(json) {
      return JSON.parse(json)
    },
    changeCardData() {
      let leafData = this.leafDataMap[this.item.id]
      if (leafData == null) {
        return
      }
      this.leafConfigData = JSON.parse(leafData[0].data)
      this.getCardData(this.leafConfigData)
    },
    cardStyle() {
      if (this.leafConfigData == null) {
        return ''
      }
      let style = ''
      if (this.leafConfigData.width != null && this.leafConfigData.width != '') {
        style += 'width:' + this.leafConfigData.width + ';'
      }
      if (this.leafConfigData.height != null && this.leafConfigData.height != '') {
        style += 'height:' + this.leafConfigData.height + ';'
      }
      return style
    },
    getCardData(leafConfigData) {
      const self = this
      let params = {
        "cardData": leafConfigData
      }
      Taro.request({url: leafConfigData.url, data: params},).then(res => {
        let result = res.data.data
        self.cardData = result
      })
    }
  },
  watch: {
    item: function (item) {
      this.changeCardData()
    },
    leafDataMap: function (leafDataMap) {
      this.changeCardData()
    }
  },
  created() {
    this.changeCardData()
  }
}
</script>
