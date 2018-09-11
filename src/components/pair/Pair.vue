<template>
  <div class="height100">
    <div class="header-container">
      <h2 class="text-center">Pair</h2>
      <h4 class="text-center" v-show="currExchange">for: {{currExchange.id}}</h4>
    </div>
    <div class="items-container">
      <h4 class="text-center" v-show="!currExchange.symbols && !errMsg">Chose an exchange</h4>
      <h4 class="text-center" v-show="errMsg">{{errMsg}}</h4>
      <ul>
        <li v-for="pair in currExchange.symbols" @click="findTrades(currExchange, pair)">{{ pair }}</li>
      </ul>
    </div>
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

.items-container > ul {
  list-style-type: none;
  padding: 0;
}

.items-container > ul > li:hover{
  cursor: pointer;
  background-color: gray;
}

</style>
