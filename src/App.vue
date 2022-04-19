<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
//<img class="h-24 w-24 rounded-3xl mt-8 mx-auto" src="src/assets/christmas selfie (2).png">
import axios from 'axios'
import GifSquare from './components/GifSquare.vue'
import SingleGif from './components/SingleGif.vue'

</script>

<template>
<div class="mx-auto max-w-5xl font-semibold text-white my-4 text-6xl">
  Gifs
</div>
<div class="mx-auto max-w-5xl my-6 shadow-lg bg-gray-900">
<div class="ml-6 text-xl text-white pt-6">
  TRENDING
</div>
  <div class="grid xl:grid-cols-5 md:grid-cols-2 sm:grid-cols-1 gap-6 place-content-center"> 
  <div v-for="gif in trendingGif" :key="gif.id">
    <GifSquare v-bind:url="gif.images.original.url" />
  </div>
  </div>
</div>
<div class="grid xl:grid-cols-2 md:grid-cols-1 mx-56 ">
<div class="h-100 w-100 px-10 py-10 mx-auto my-6 max-w-sm bg-gray-900 grid place-content-center">
  <div class="my-4 text-xl text-white">
    RANDOM
  </div>
    <SingleGif v-bind:url="randomGif" />
    <button @click="refresh" class="mt-14 mb-6 rounded-md bg-blue-400 hover:scale-110 transform transition duration-300">
      REFRESH
    </button>
</div>
<div class="h-100 w-100 px-10 py-10 mx-auto my-6 max-w-sm bg-gray-900 grid place-content-center">
  <div class="mb-6 text-xl text-white">
    SEARCH
  </div>
    <SingleGif v-bind:url="searchGif" />
    <input v-model="searchTerm" class="mt-14"/>
    <button @click="search" class="mt-8 mb-6 rounded-md bg-blue-400 ">
      SEARCH
    </button>
</div>
</div>
</template>

<script>
export default {
    data () {
    return {
      randomGif: null,
      trendingGif: null,
      searchGif: null,
      searchTerm: null
    }
  },
  mounted() {
    axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&limit=10')
      .then(response => (this.randomGif = response.data.data.images.original.url))

    axios
      .get('https://api.giphy.com/v1/gifs/trending?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&limit=10&rating=r')
      .then(response => (this.trendingGif = response.data.data))

    axios
      .get('https://api.giphy.com/v1/gifs/search?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&q=dog&limit=1&offset=0&rating=g&lang=en')
      .then(response => (this.searchGif = response.data.data[0].images.original.url))
  },
  methods:{
    refresh(){
      axios
      .get('https://api.giphy.com/v1/gifs/random?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&limit=10')
      .then(response => (this.randomGif = response.data.data.images.original.url))
    },
    search(){
      axios
      .get('https://api.giphy.com/v1/gifs/search?api_key=91guYgr3J403zwIRDi0ZZNtUsyVZLPiV&q=' + this.searchTerm +'&limit=1&offset=0&rating=g&lang=en')
      .then(response => (this.searchGif = response.data.data[0].images.original.url))
    }
  }
}
</script>