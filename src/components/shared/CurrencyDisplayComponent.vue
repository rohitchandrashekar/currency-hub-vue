<template>
  <div>
    <b-card :title="baseCurrency" :sub-title="time">
      <b-card-text
        v-for="(item, index) in currentExchangeRates"
        v-bind:key="item"
      >{{ index }} - {{ currentExchangeRates[index] }}</b-card-text>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "DisplayCurrency",
  props: ["currentExchangeData"],
  watch: {
    currentExchangeData: function(newValue) {
      this.currentExchangeRates = newValue.rates;
      this.time = newValue.date;
      this.baseCurrency = newValue.base;
    }
  },
  data() {
    return {
      baseCurrency: this.currentExchangeData.base,
      time: this.currentExchangeData.date,
      currentExchangeRates: this.currentExchangeData
        ? this.currentExchangeData.rates
        : ""
    };
  },

  methods: {}
};
</script>

<style>
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
