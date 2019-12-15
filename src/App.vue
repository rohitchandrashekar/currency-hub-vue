<template>
  <div id="app">
    <img src="./assets/logo.png" />
    <h1>{{ msg }}</h1>
    <div>
      <b-tabs content-class="mt-3" fill>
        <b-tab title="View Exchange Rates" active>
          <SelectCurrency @handleChangeEvent="getCurrentValue"></SelectCurrency>
          <DisplayValues v-if="currentExchangeData" :currentExchangeData="currentExchangeData"></DisplayValues>
        </b-tab>
        <b-tab title="Convert Currencies">
          <SelectCurrency @handleChangeEvent="getConversionValue"></SelectCurrency>
          <p>Work In Progress</p>
        </b-tab>
        <b-tab title="View exchange rate graph">
          <SelectCurrency @handleChangeEvent="getHistoricValue"></SelectCurrency>
          <DatePicker @handleDateChangeEvent="getDateFilter"></DatePicker>
          <LineChart :chartdata="chartData" :options="chartOptions"></LineChart>
        </b-tab>
      </b-tabs>
    </div>
  </div>
</template>

<script>
import SelectCurrency from "./components/shared/DropDownComponent";
import DisplayValues from "./components/shared/CurrencyDisplayComponent";
import LineChart from "./components/shared/LineChartComponent";
import DatePicker from "./components/shared/DatePicker";
import { HTTP } from "./http-common";
console.log(SelectCurrency);
export default {
  name: "app",
  data() {
    return {
      msg: "Currency Information",
      currentDate: "",
      currentExchangeData: "",
      chartData: {},
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      },
      selectedCurrencyForHistoric: ""
    };
  },
  components: {
    SelectCurrency,
    DisplayValues,
    LineChart,
    DatePicker
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
    },
    getConversionValue(newValue) {
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
    },
    getHistoricValue(newValue) {
      this.selectedCurrencyForHistoric = newValue;
    },
    getDateFilter(newValue) {
      if (newValue.from && newValue.to && this.selectedCurrencyForHistoric) {
        HTTP.get(
          `/${newValue.from}..${newValue.to}?to=${this.selectedCurrencyForHistoric}`
        )
          .then(response => {
            this.transformDataSet(response.data.rates);
          })
          .catch(error => {
            console.log(error);
          });
      }
    },
    transformDataSet(rates) {
      const transformedData =  {
        labels: Object.keys(rates),
        datasets: [{
            label: 'Currency Value',
            data: [],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)'
            ],
            borderWidth: 1
        }]
      }
      for( let key in rates) {
        transformedData.datasets[0].data.push(rates[key][this.selectedCurrencyForHistoric]);
      }
      this.chartData = transformedData;

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
.custom-select {
  width: 25%;
}
</style>
