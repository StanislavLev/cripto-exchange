<template>
  <div>
    <h2>PAIR</h2>
    <h4 v-show="!currExchange.symbols && !errMsg">Chose an exchange</h4>
    <h4 v-show="errMsg">{{errMsg}}</h4>
    <h4 v-for="pair in currExchange.symbols" @click="findTrades(currExchange, pair)">{{ pair }}</h4>
  </div>
</template>

<script>

import {bus} from '@/main.js';

export default {
  name: 'Pair',
  data() {
    return {
      errMsg: '',
      currExchange: {},
    };
  },
  methods: {
    findTrades(exchange4trades, pair4trades) {
      bus.$emit('PairChosen', exchange4trades, pair4trades);
    },
  },
  created(){
    bus.$on('exchangeChosen', (exchange)=>{
      this.currExchange = exchange;
      this.errMsg = '';
    });
    bus.$on('exchangeChosenErr', (err)=>{
      this.errMsg = err;
      this.currExchange = {};
    });
  },
};
</script>

<style scoped>

</style>
