<template>
  <div v-if='beer'>
      <h3>Name: {{ beer.name}}</h3>
      <h4>Tag: {{ beer.tagline }}</h4>
      
      <div id="favourite-button" v-if="beer">
            <button v-on:click="handleClick">Add {{beer.name}} to your favourite beers?</button>
        </div>
    <img :src="beer.image_url">
<!-- v-if="!favouriteBeers.includes(beer)" -->
      
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
        handleClick() {
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