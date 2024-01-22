<template>
  <div class="flex gap-2 mt-2 pb-4 mx-auto w-fit border-gray-700 border-b-[1px]">
    <button v-if="page > 1" role="button" aria-label="Search" class="
      bg-transparent
      hover:bg-blue-500
      focus:border-blue-600
      hover:border-blue-300
      hover:text-white
      border-gray-700
      border
      focus:outline-none 
      transition 
      duration-150 
      ease-in-out 
      rounded 
      text-gray-600 
      dark:text-gray-400
      px-8 
      py-2 
      text-sm
    " type="button" @click="$emit('change', page-1)">{{ '<' }}</button>

    <p class=" text-gray-600 
    dark:text-gray-400
    px-8 
    py-2 
    text-sm">
      {{ page }}
    </p>

    <button v-if="page < maxPage" role="button" aria-label="Search" class="
      bg-transparent
      hover:bg-blue-500
      focus:border-blue-600
      hover:border-blue-300
      hover:text-white
      border-gray-700
      border
      focus:outline-none 
      transition 
      duration-150 
      ease-in-out 
      rounded 
      text-gray-600 
      dark:text-gray-400
      px-8 
      py-2 
      text-sm
    " type="button" @click="$emit('change', page+1)">{{ '>' }}</button>
  </div>


  
      
</template>

<script setup>
defineProps({
  page: Number,
  maxPage: Number,
})
</script>