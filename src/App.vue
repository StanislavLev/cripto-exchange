<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-sm-3 main-col">
        <exchange></exchange>
      </div>
      <div class="col-sm-3 main-col" >
        <pair></pair>
      </div>
      <div class="col-sm-6 main-col">
        <trades></trades>
      </div>
    </div>
  </div>
</template>

<script>

import Exchange   from '@/components/exchange/Exchange.vue';
import Pair       from '@/components/pair/Pair.vue';
import Trades     from '@/components/trades/Trades.vue';

export default {
  name: 'App',
  components: {
    'exchange' :  Exchange,
    'pair'     :  Pair,
    'trades'   :  Trades,
  },
};

</script>

<style scoped>

.container-fluid {
  height: 100%;
}

.row {
  height: 100%;
}

.col-sm-4 {
  border: #272727 solid 1px;
}

</style>
