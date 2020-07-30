<template>
  <div v-if='beer'>
      <h3>Name: {{ beer.name}}</h3>
      <h4>Tag: {{ beer.tagline }}</h4>
      <img :src="beer.image_url">
  </div>
</template>

<script>
import {eventBus} from '@/main.js';

export default {
    name: 'beer-detail',
    data() {
        return {
            beer: null
        }
    },
    mounted() {
        eventBus.$on('beer-select', (beer) => {this.beer = beer})
    },
    props: ['favourite-beer'],
    methods: {
        handleSubmit() {
            eventBus.$emit('favourite-beer', this.beer)
        }
    }

}
</script>

<style>
    img {
        width: 125px;
        height: 300px;
    }
</style>