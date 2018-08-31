<template>
  <div>
    <h1>{{ pair }}</h1>
  </div>
</template>

<script>

import {bus} from '@/main.js';

export default {
  name: 'Pair',
  data() {
    return {
      pair: 'BTC/USD',
    };
  },
  created(){
    bus.$on('exchangeChosen', (data)=>{
      this.pair = data;
    })
  },
};
</script>

<style scoped>

</style>
