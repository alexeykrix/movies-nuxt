<template>
  <div class="min-h-lvh bg-white dark:bg-gray-800">

    <a @click="goBack" class="text-white mt-6 ml-6" href="/">Go back</a>

    <div class="flex flex-col w-[500px] p-6" >
      
      <img :src="img(data?.poster_path)" alt="">
      <p class="text-2xl text-white">{{ data?.title }}</p>
  
      <p class="text-lg text-white">{{ data?.overview }}</p>
  
  
      <div class="flex gap-4">
        <p class="text-lg text-gray-400">{{ formatDate(data?.release_date) }}</p>
        <p class="text-lg text-gray-400">{{ data?.vote_average }}</p>
      </div>
  
      <div class="flex gap-4">
        <span class="text-l text-gray-400" v-for="genre in data?.genres" :key="genre.id">{{ genre.name }}</span>
      </div>
    </div>


  </div>
</template>

<script setup>

const { id } = useRoute().params
const router = useRouter();
const goBack = () =>{
  router.go(-1)
}

if (!id) throw new Error(404)

const img = path => 'https://image.tmdb.org/t/p/w220_and_h330_face' + path
const formatDate = dateStr => {
  const date = new Date(dateStr)

  return date.toLocaleString('en-US', {
    month: "short",
    year: "numeric",
  })
}

const getData = async (id) => {

  const config = useRuntimeConfig()
  const url = `https://api.themoviedb.org/3/movie/${id}?include_adult=true&language=en-US`

  const options = {
    method: 'GET',
    headers: {
      accept: 'application/json',
      Authorization: 'Bearer ' + config.public.MOVIE_TOKEN
    }
  };

  return fetch(url, options)
    .then(res => res.json())
    .catch(err => {
      console.error('error:' + err)
      throw new Error(404)
    }
  )
}


const { data, pending, error, refresh } = await useAsyncData(
  'id',
  () => getData(id)
)


</script>