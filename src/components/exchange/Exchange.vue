<template>
  <div>
    <h2>EXCHANGE</h2>
    <h6 v-for="exchange in exchanges" @click="findPair(exchange)">{{ exchange }}</h6>
  </div>
</template>

<script>

import {bus} from '@/main.js';

export default {
  name: 'Exchange',
  data() {
    return {
      exchanges: ccxt.exchanges,
    };
  },
  methods: {
    findPair(exchange) {
      bus.$emit('exchangeChosen', exchange);
    },
  },
};
</script>

<style scoped>

</style>
