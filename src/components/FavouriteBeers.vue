<template>
<div v-if="favBeers">
    <h3>Favourite Beers:</h3>
    <ul>
        <li v-for="(beer, index) in favBeers" :beer="beer" :key="index">{{beer.name}}</li>
    </ul>
</div>
  
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: 'favourite-beers',
    data() {
        return {
            favBeers: []
        }
    },
    mounted() {
        eventBus.$on('favourite-beer', (favBeers) => {this.favBeers.push(favBeers)})
    }

}
</script>

<style>

</style>