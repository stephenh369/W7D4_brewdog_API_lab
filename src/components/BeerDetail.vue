<template>
  <div v-if='beer'>
      <h3>Name: {{ beer.name}}</h3>
      <h4>Tag: {{ beer.tagline }}</h4>
      
      <div id="favourite-button">
            <button v-if="!favBeers.includes(beer)" v-on:click="handleClick">Add {{beer.name}} to your favourite beers?</button>
            <button v-if="favBeers.includes(beer)" v-on:click="handleRemove">Remove {{beer.name}} from your favourite beers?</button>
      </div>
      <img :src="beer.image_url">

      <div id="ingredients">
          <ul v-for="(type, index) in beer.ingredients" :type="type" :key="index">
              <li v-for="(i, index) in type" :i="i" :key="index">{{i}}</li>
          </ul>
          <!-- <p v-for="(i, index) in beer.ingredients.malt" :i="i" :key="index">{{i.name}}</p> -->
      </div>

      
  </div>
</template>

<script>
import {eventBus} from '@/main.js';
import FavouriteBeers from './FavouriteBeers.vue';

export default {
    name: 'beer-detail',
    data() {
        return {
            beer: null,
            favBeers: []
        }
    },
    mounted() {
        eventBus.$on('beer-select', (beer) => {this.beer = beer}),
        eventBus.$on('favourite-beers', (beers) => {this.favBeers = beers})
    },
    props: ['favourite-beer'],
    methods: {
        handleClick() {
            eventBus.$emit('favourite-beer', this.beer)
        },
        handleRemove() {
            eventBus.$emit('unfavourite-beer', this.beer)
        }
    },
    components: {
        'favourite-beers' : FavouriteBeers
    }

}
</script>

<style>
    img {
        width: 125px;
        height: 300px;
    }
</style>