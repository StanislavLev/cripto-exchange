<template>
  <div>
    <h2>TRADES : {{dateNow.getUTCHours()}} : {{dateNow.getUTCMinutes()}} : {{dateNow.getUTCSeconds()}}</h2>
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
      dateNow: new Date(),
      errMsg: '',
      exchange: {},
      pair: '',
      allTrades: [],
      limit: 20,
      fetchTradesInterval: undefined,
    };
  },
  created(){
    bus.$on('PairChosen', (exchange, pair)=>{
      this.allTrades = [];
      this.errMsg = '';
      this.exchange = exchange;
      this.pair = pair;
      let since = undefined;
      if(this.fetchTradesInterval){
        clearInterval(this.fetchTradesInterval);
      }
      this.fetchTradesInterval = setInterval(
        async () => {
          if (this.exchange.has['fetchTrades']) {
            try {
              this.allTrades = await exchange.fetchTrades (this.pair, since, this.limit);
              this.dateNow = new Date();
            } catch(err) {
              this.errMsg = "Failed to fetch the trades info, please try another pair or exchange."
              this.allTrades = [];
              if(this.fetchTradesInterval){
                clearInterval(this.fetchTradesInterval);
              }
            }
          }
        }, 
      2000);
    });
    bus.$on('exchangeChosenErr', (err)=>{
      this.allTrades = [];
      this.errMsg = '';
      if(this.fetchTradesInterval){
        clearInterval(this.fetchTradesInterval);
      }
    });
  },
};
</script>

<style scoped>

</style>
