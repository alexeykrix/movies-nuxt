<template>
  <nuxt-link :to="`/movie/${ data.id }`" class="group group-hover:bg-opacity-60 transition duration-500 relative bg-gray-50 dark:bg-gray-800 dark:hover:bg-gray-700 flex flex-col justify-center items-center">
      <img class="group-hover:opacity-60 transition duration-500 mb-2 w-full" :src="img(data?.poster_path)" alt="sofa-2" />
      <div class="absolute sm:top-8 top-4 left-4 sm:left-8 flex justify-start items-start flex-col space-y-2">
        <p class="group-hover:opacity-60 transition duration-500 text-xs leading-5 text-gray-600 dark:text-white">
          {{ formatDate(data?.release_date) }}
        </p>
      </div>
      <div class="py-1 px-1 w-full">
        <p class="group-hover:opacity-60 h-10 transition duration-500 text-l leading-5 text-gray-600 dark:text-white">
          {{ data?.title }}
        </p>
      </div>
  </nuxt-link>
</template>
<script setup>
defineProps({
  data: Object,
})

const img = path => 'https://image.tmdb.org/t/p/w220_and_h330_face' + path
const formatDate = dateStr => {
  const date = new Date(dateStr)

  return date.toLocaleString('en-US', {
    month: "short",
    year: "numeric",
  })
}

</script>