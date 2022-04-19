<script setup>

defineProps({
  url: String
})

</script>

<template>
    <div class="h-100 w-100 px-6 py-6 flex place-content-center">
    <img class="h-80 w-80 shadow-md hover:shadow-xl hover:scale-110 transform transition duration-500" v-bind:src='url'>
    </div>
</template>