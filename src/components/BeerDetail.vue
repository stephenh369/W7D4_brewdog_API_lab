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
          <h4>Malts</h4>
          <ul>
              <li v-for="(malt, index) in filterMaltDups" :malt="malt" :key="index">{{malt}}</li>
          </ul>
          <h4>Hops</h4>
            <ul>
              <li v-for="(hop, index) in filterHopDups" :hop="hop" :key="index">{{hop}}</li>
            </ul>
            <h4>Yeast</h4>
            <ul>
                <li>{{beer.ingredients.yeast}}</li>
            </ul>
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
    computed: {
        filterMaltDups() {
            const array = this.beer.ingredients.malt;
            const newArray = array.map((i) => i.name);
            const filteredArray = newArray.filter((i, index) => newArray.indexOf(i) === index);
            return filteredArray;
        },
        filterHopDups() {
            const array = this.beer.ingredients.hops;
            const newArray = array.map((i) => i.name);
            const filteredArray = newArray.filter((i, index) => newArray.indexOf(i) === index);
            return filteredArray;
        }
    },
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
        margin: 10px;
        width: 125px;
        height: 300px;
    }
    #ingredients {
        display: inline-block;
        margin-top: 10px;
        margin-left: 25px;
    }
</style>