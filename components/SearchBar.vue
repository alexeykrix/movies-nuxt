<template>
  <div class="flex gap-2 px-3 py-4 mb-4 border-gray-700 border-b-[1px] sticky top-0 z-10 bg-gray-800 bg-opacity-70 backdrop-blur-lg">
    <input v-model="searchInp" tabindex="0" type="text" id="search" name="Search query" class="
      w-full 
      border 
      border-gray-500 
      px-3 
      py-3 
      shadow-sm 
      rounded 
      text-sm 
      hover:border-blue-300
      focus:outline-none 
      focus:border-blue-600 
      bg-transparent 
      placeholder-gray-500 
      text-gray-400
    " placeholder="Movie, genre, actor" />

    <button role="button" aria-label="Search" class="
      bg-transparent
      hover:bg-blue-500
      focus:border-blue-600
      hover:border-blue-300
      hover:text-white
      border-gray-500
      border
      focus:outline-none 
      transition 
      duration-150 
      ease-in-out 
      rounded
      text-gray-400
      px-8 
      py-2 
      text-sm
    " type="button" @click="$emit('search', searchInp)">Search</button>
    
  </div>


  
      
</template>

<script setup>
const searchInp = ref('')
</script>