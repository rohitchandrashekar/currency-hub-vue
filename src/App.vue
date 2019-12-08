<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <h1>{{ msg }}</h1>
    <div>
      <b-tabs content-class="mt-3" fill>
        <b-tab title="View Exchange Rates" active>
          <p>Select Currency</p>
          <SelectCurrency @handleChangeEvent="getCurrentValue"></SelectCurrency>
           <DisplayValues v-if="currentExchangeData" :currentExchangeData="currentExchangeData">
          </DisplayValues>
        </b-tab>
        <b-tab title="Convert Currencies">
          <p>Work In Progress</p>
        </b-tab>
        <b-tab title="View exchange rate graph">
          <p>Work In Progress</p>
        </b-tab>
      </b-tabs>
    </div>
  </div>
</template>

<script>
import SelectCurrency from "./components/shared/DropDownComponent";
import DisplayValues from "./components/shared/CurrencyDisplayComponent";
import { HTTP } from "./http-common";
console.log(SelectCurrency);
export default {
  name: "app",
  data() {
    return {
      msg: "Currency Information",
      currentDate: "",
      currentExchangeData: ''
    };
  },
  components: {
    SelectCurrency,
    DisplayValues
  },
  methods: {
    getCurrentValue(newValue) {
      /* this.selectedCurrency = newValue; */
      console.log(newValue);
      HTTP.get(`/latest?from=${newValue}`)
        .then(response => {
          console.log(response.data);
          this.currentExchangeData = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  watch: {}
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
