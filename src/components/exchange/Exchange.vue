<template>
  <div>
    <h2>EXCHANGE</h2>
    <h6 v-for="exchange in exchanges">{{ exchange }}</h6>
  </div>
</template>

<script>
export default {
  name: 'Exchange',
  data() {
    return {
      exchanges: ccxt.exchanges,
    };
  },
  methods: {
    
  },
};
</script>

<style scoped>

</style>
