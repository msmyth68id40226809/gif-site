<script setup>

defineProps({
  url: String
})

</script>

<template>
    <div class="h-50 w-50 px-6 py-6 flex place-content-center">
    <img class="h-40 w-40 shadow-md hover:shadow-xl hover:scale-125 transform transition duration-500" v-bind:src='url'>
    </div>
</template>