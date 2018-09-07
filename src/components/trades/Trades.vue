<template>
  <div>
    <h2>TRADES</h2>
    <h4 v-show="errMsg">{{errMsg}}</h4>
    <h4 v-for="trade in allTrades">{{ trade.amount }} : {{ trade.price }} : {{ trade.datetime }}<br /> </h4>
  </div>
</template>

<script>

import {bus} from '@/main.js';

export default {
  name: 'Trades',
  data() {
    return {
      errMsg: '',
      exchange: {},
      pair: '',
      allTrades: [],
      limit: 20,
    };
  },
  created(){
    bus.$on('PairChosen', (exchange, pair)=>{
      this.allTrades = [];
      this.errMsg = '';
      this.exchange = exchange;
      this.pair = pair;
      let since = undefined;
      (async () => {
        if (this.exchange.has['fetchTrades']) {
          try {
            this.allTrades = await exchange.fetchTrades (this.pair, since, this.limit);
          } catch(err) {
            this.errMsg = "Failed to fetch the trades info, please try another pair or exchange."
          }
        }
      })();
    });
    bus.$on('exchangeChosenErr', (err)=>{
      this.allTrades = [];
    });
  },
};
</script>

<style scoped>

</style>
