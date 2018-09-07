<template>
  <div>
    <h2>EXCHANGE</h2>
    <input type="text" v-model="exchangeFilter"></input>
    <h6 v-for="exchange in exchanges" @click="findPair(exchange)" v-show="exchange.indexOf(exchangeFilter)!=-1">{{ exchange }}</h6>
  </div>
</template>

<script>

import {bus} from '@/main.js';

export default {
  name: 'Exchange',
  data() {
    return {
      exchanges: ccxt.exchanges,
      exchangeFilter: '',
    };
  },
  methods: {
    findPair(exchange4pair) {
      (async () => {
        let currExchange = new ccxt[exchange4pair]();
        currExchange.enableRateLimit = true;
        try {
          await currExchange.loadMarkets();
          bus.$emit('exchangeChosen', currExchange);
        } catch(err) {
          bus.$emit('exchangeChosenErr', "Failed to fetch the exchange info, please try another one.");
        }      
      })();
    },
  },
};
</script>

<style scoped>

</style>
