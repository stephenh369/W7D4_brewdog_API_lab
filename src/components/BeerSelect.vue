<template>
  
</template>

<script>

import {eventBus} from '@/main.js';

export default {
  name: 'beers-select',
  data() {
    return {
      selectedBeer: null
    };
  },
  props: ['beers'],
  methods: {
    handleChange() {
      eventBus.$emit('beer-select', this.selectedBeer)
    }
  }
}
</script>

<style>

</style>