<template>
  <view style="background: #f1f1f1;">
    <MyCard :item="item"
            :leaf-data-map="leafDataMap"></MyCard>
  </view>
</template>

<script>
import MyCard from "../../components/my.card/player.card";

export default {
  components: {MyCard},
  name: "Waterfall",
  props: {
    item: null,
    leafDataMap: null
  }
}
</script>

<style scoped>

</style>
