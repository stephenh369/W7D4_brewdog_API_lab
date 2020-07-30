<template>
  
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
    props: ['beer'],
    methods: {
        handleSubmit() {
            eventBus.$emit('favourite-beer', this.beer)
        }
    }

}
</script>

<style>

</style>