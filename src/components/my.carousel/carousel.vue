<template>
  <view>
    <swiper v-show="item.type === 'Carousel'"
            indicatorColor='#999'
            indicatorActiveColor='#333'
            :circular=true
            :autoplay=true
            :indicatorDots=true>
      <swiper-item v-for="(leafData, index) in  leafDataMap[item.id]" :key="index">
        <image :src="dataToObject(leafData.data).imgSrc" class="slide-image"
               @tap="clickSwiperItem(leafData.data)"/>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>


export default {
  name: "MyCarousel",
  props: {
    item: null,
    leafDataMap: null
  },
  data() {
    return {}
  },
  methods: {
    dataToObject(json) {
      return JSON.parse(json)
    },
    clickSwiperItem(json) {
      console.log(json)
    },
  }
}
</script>

<style scoped>

</style>
