<template>
  <div>
    <date-pick v-model="fromDate"></date-pick>
    <date-pick v-model="toDate"></date-pick>
    <b-button variant="outline-primary" v-on:click="sendDateEvent">Show</b-button>
  </div>
</template>

<script>
import DatePick from "vue-date-pick";
import "vue-date-pick/dist/vueDatePick.css";

export default {
  components: { DatePick },
  data: () => ({
    fromDate: "2019-01-01",
    toDate: "2019-02-01",
  }),
  methods: {
      sendDateEvent :  function() {
          console.log(this.fromDate,this.toDate);
           this.$emit('handleDateChangeEvent',{from:this.fromDate,to:this.toDate});
      }
  },
  watch:{
    fromDate: function(nv) {
      console.log(nv);
    }
  }
};
</script>
<style scoped>
.vdpArrowPrev:after {
    border-right-color: #cc99cd;
}

.vdpArrowNext:after {
    border-left-color: #cc99cd;
}

.vdpCell.selectable:hover .vdpCellContent,
.vdpCell.selected .vdpCellContent {
    background: #329628;
}

.vdpCell.today {
    color: #cc99cd;
}

.vdpTimeUnit > input:hover,
.vdpTimeUnit > input:focus {
    border-bottom-color: #cc99cd;
}
</style>