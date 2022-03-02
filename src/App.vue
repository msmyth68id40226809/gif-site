<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
//<img class="h-24 w-24 rounded-3xl mt-8 mx-auto" src="src/assets/christmas selfie (2).png">
import axios from 'axios'
</script>

<template>
<div class="mx-auto max-w-md pb-12"> 
  <div class="max-w-sm mx-auto">
    <div class=" text-4xl flex justify-center font-sans text-purple-600 mt-4">GIF Generator</div>
  </div>
  <div class="">
    <img class="mx-auto h-32 w-32 mt-6" v-bind:src='randomGif'>
  </div>
  <div>
  <div v-for="gif in trendingGif" :key="gif.id" class="flex columns-3">
    <img class="h-40 w-40 mt-6 px-1 col-span-1 shadow-md hover:shadow-xl hover:scale-125 transform transition duration-500" v-bind:src='gif.images.original.url'>
  </div>
  </div>
</div>
</template>

<script>
export default {
    data () {
    return {
      randomGif: null,
      trendingGif: null
    }
  },
  created () {
    axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&limit=10')
      .then(response => (this.randomGif = response.data.data.images.original.url))

    axios
      .get('https://api.giphy.com/v1/gifs/trending?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&limit=10&rating=g')
      .then(response => (this.trendingGif = response.data.data))
  }
}
</script>