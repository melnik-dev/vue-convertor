<template>
  <div class="App">
    <convertBlock v-model="fromPrice" :currency="fromCurrency" @onChangeCurrency="fromChangeCurrency" @onChangeValue="fromChangePrice"/>
    <convertBlock v-model="toPrice" :currency="toCurrency" @onChangeCurrency="toChangeCurrency" @onChangeValue="toChangePrice"/>
  </div>
</template>

<script>
import convertBlock from './components/convertBlock.vue'

export default {
  name: 'App',
  components: {
    convertBlock
  },
  data() {
    return {
      rates: {},
      fromCurrency: "RUB",
      toCurrency: "USD",
      fromPrice: 0,
      toPrice: 0
    }
  },
  methods: {
    fromChangeCurrency(cur) {
      this.fromCurrency = cur;
      this.fromChangePrice(this.fromPrice);
      console.log(this.fromCurrency);
    },
    toChangeCurrency(cur) {
      this.toCurrency = cur
      this.toChangePrice(this.toPrice);
      console.log(this.toCurrency);
    },
    fromChangePrice(value) {
      const price = value / this.rates[this.fromCurrency];
      const result = price * this.rates[this.toCurrency];
      this.toPrice = result;

    },
    toChangePrice(value) {
      const result = (this.rates[this.fromCurrency] / this.rates[this.toCurrency]) * value;
      this.fromPrice = result;
    }
  },
  created() {
    fetch('https://cdn.cur.su/api/latest.json')
          .then((res) => res.json())
          .then((json) => {
              this.rates = json.rates;
              console.log(this.rates);
          }).catch(err => {
      console.warn(err);
      alert("не удалось получить инфорамцию")
    })
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');
body {
  background-color: #f9f2ed;
}
* {
  font-family: 'Inter', system-ui !important;
  box-sizing: border-box;
  user-select: none;
}
.App {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 30px;
  width: 800px;
  margin: 100px auto;
  background-color: #fff;
  padding: 30px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.05);
  border-radius: 15px;
}
.block input {
  border: 1px solid rgba(0, 0, 0, 0.1);
  font-size: 3rem;
  font-weight: bold;
  padding: 20px 20px;
  letter-spacing: 1.3px;
  outline: none;
  margin-top: 20px;
  border-radius: 5px;
  width: 100%;
}
.currencies {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 0;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 5px;
  overflow: hidden;
}
.currencies li {
  display: inline-flex;
  padding: 10px 20px;
  border-right: 1px solid rgba(0, 0, 0, 0.05);
  cursor: pointer;
  justify-content: center;
  flex: 1;
}
.currencies li:hover {
  background-color: rgba(0, 0, 0, 0.03);
}
.currencies li:active {
  background-color: rgba(0, 0, 0, 0.05);
}
.currencies li.active {
  background-color: #16b67f;
  color: #fff;
}
.currencies li:last-of-type {
  display: inline-flex;
  align-items: center;
  flex: 0 0 50px;
  border-right: 0;
}
.currencies li:last-of-type svg {
  width: 16px;
  height: 16px;
}

</style>
