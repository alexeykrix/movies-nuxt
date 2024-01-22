<template>
  <div class=" min-h-lvh bg-white dark:bg-gray-800">    
    <SearchBar @search="search" />

    <FilmsGrid :data="films" />

    <GridPagination :page="currentPage" :maxPage="totalPages" @change="changePage" />
  
  </div>
</template>


<script setup>
const films = ref([])
const currentPage = ref(1)
const totalPages = ref(0)
const totalResults = ref(0)

const searchQuery = ref('')


const getData = async (args) => {

  const type = args ? 'search' : 'discover'

  const config = useRuntimeConfig()

  const url = `https://api.themoviedb.org/3/${type}/movie?include_adult=true&language=en-US&page=${ currentPage.value }${
    searchQuery.value ? '&query=' + searchQuery.value.split(' ').join('+') : ''
  }`

  const options = {
    method: 'GET',
    headers: {
      accept: 'application/json',
      Authorization: 'Bearer ' + config.public.MOVIE_TOKEN
    }
  };

  return fetch(url, options)
    .then(res => res.json())
    .catch(err => console.error('error:' + err))
  
}

const setResults = (data) => {
  const { page, total_pages, total_results, results } = data

  if (page === 1) {
    films.value = []
  }
  films.value.push(...results) 
  currentPage.value = page
  totalPages.value = total_pages
  totalResults.value = total_results
}

const fetchData = async (args) => {
  setResults(
    await getData(args)
  )
}


const changePage = (page) => {
  if (page < totalPages.value) {
    currentPage.value = page
  }

  fetchData(searchQuery.value)
} 


const search = async (args) => {
  if (args) {
    searchQuery.value = args
  }

  changePage(1)
}

await fetchData()


</script>