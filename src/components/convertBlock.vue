<template lang="pug">
.block
  ul.currencies
    li(v-for="cur in defaultCurrencies" :key="cur" @click="onChangeCurrency(cur)" :class="currency === cur ? 'active' : ''") {{cur}}
    li
      svg(height="50px" viewBox="0 0 50 50" width="50px")
        rect(fill="none" height="50" width="50")
        polygon(points="47.25,15 45.164,12.914 25,33.078 4.836,12.914 2.75,15 25,37.25 ")
  input(@change="onChangeValue(value)" v-model="value" type="number" placeholder="currency")
</template>

<script>

export default {
  name: "convertBlock",
  props:["value", "currency"],
  emits: ["onChangeCurrency", "onChangeValue"],
  data() {
    return {
      defaultCurrencies: ["RUB", "USD", "EUR", "GBR"],
    }
  },
  methods:{
    onChangeCurrency(cur) {
      this.$emit("onChangeCurrency", cur);
    },
    onChangeValue(value) {
      this.$emit("onChangeValue", value);
    }
  }
}
</script>

<style scoped>

</style>