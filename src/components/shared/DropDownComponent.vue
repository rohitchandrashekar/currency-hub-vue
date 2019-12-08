<template>
  <div>
    <b-form-select
      id="currencySelect"
      text="Select Currency"
      class="m-md-2"
      @change="handleChangeEvent"
    >
      <option v-bind:value="currency" v-for="(currencyName, currency) in currencyList" v-bind:key="currency">{{currencyName}}</option>
    </b-form-select>
  </div>
</template>

<script>
export default {
  name: "SelectCurrency",
  data() {
    return {
      msg: "Currency Information",
      currencyList: {},
    };
  },
  methods: {
      handleChangeEvent: function(event) {
          console.log(event);
          this.$emit('handleChangeEvent',event);
          
      }
  },
  created() {
    this.currencyList = {
      AUD: "Australian Dollar",
      BGN: "Bulgarian Lev",
      BRL: "Brazilian Real",
      CAD: "Canadian Dollar",
      CHF: "Swiss Franc",
      CNY: "Chinese Renminbi Yuan",
      CZK: "Czech Koruna",
      DKK: "Danish Krone",
      EUR: "Euro",
      GBP: "British Pound",
      HKD: "Hong Kong Dollar",
      HRK: "Croatian Kuna",
      HUF: "Hungarian Forint",
      IDR: "Indonesian Rupiah",
      ILS: "Israeli New Sheqel",
      INR: "Indian Rupee",
      ISK: "Icelandic Króna",
      JPY: "Japanese Yen",
      KRW: "South Korean Won",
      MXN: "Mexican Peso",
      MYR: "Malaysian Ringgit",
      NOK: "Norwegian Krone",
      NZD: "New Zealand Dollar",
      PHP: "Philippine Peso",
      PLN: "Polish Złoty",
      RON: "Romanian Leu",
      RUB: "Russian Ruble",
      SEK: "Swedish Krona",
      SGD: "Singapore Dollar",
      THB: "Thai Baht",
      TRY: "Turkish Lira",
      USD: "United States Dollar",
      ZAR: "South African Rand"
    };
    /* HTTP.get('/currencies').then((response)=> {
        console.log(response.data);
        this.currencyList = response.data;
      }).catch((error)=> {
        console.log(error);
      }) */
  }
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
