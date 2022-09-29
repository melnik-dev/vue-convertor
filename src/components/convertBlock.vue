<template lang="pug">
.block
  ul.currencies
    li(v-for="cur in defaultCurrencies" :key="cur" @click="onChangeCurrency(cur)" :class="currency === cur ? 'active' : ''") {{cur}}
    li
      svg(height="50px" viewBox="0 0 50 50" width="50px")
        rect(fill="none" height="50" width="50")
        polygon(points="47.25,15 45.164,12.914 25,33.078 4.836,12.914 2.75,15 25,37.25 ")
  input(:value="modelValue" @input="$emit('update:modelValue', $event.target.value)" @change="onChangeValue(modelValue)" type="number" placeholder="0")
</template>

<script>

export default {
  name: "convertBlock",
  props:["modelValue", "currency"],
  emits: ["onChangeCurrency", "onChangeValue", "update:modelValue"],
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