<template>
<div>
  <select @change="handleChange" v-model="selectedBeer">
    <option v-for="(beer, index) in beers" :beer="beer" :key="index" v-bind:value="beer">{{beer.name}}</option>
  </select>
</div>
  
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