<template>
  <div class="grid px-3 grid-cols-2 lg:grid-cols-4 gap-x-4 gap-y-4 items-center">
    <FilmCard v-for="film in data" :key="film.id" :data="film" />
  </div>
</template>

<script setup>
defineProps({
  data: Array
})

</script>