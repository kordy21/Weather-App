<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input type="text" v-model="searchQuery" @input="getSearchReasults" placeholder="Search for a city or state" class="py-2
      px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]">

      <ul class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px] ">
        <li class="py-2 cursor-pointer" v-for="SearchResult in mapboxSearchResults" :key="SearchResult.id" >
          {{ SearchResult.place_name }}
        </li>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from 'axios';


  const mapboxAPIKey ="pk.eyJ1IjoibW9oYW1lZDE5OTkiLCJhIjoiY2xwMW1ucGtkMGcwcjJrcW9qbzB5dXQwMyJ9.I2RMdhZXBmb6dimgyUcqxw"
  const searchQuery = ref("");
  const queryTimeout = ref(null);
  const mapboxSearchResults =ref(null);

  const getSearchReasults = ()=>{
    clearTimeout(queryTimeout.value);
    queryTimeout.value = setTimeout( async ()=>{
      if(searchQuery.value !==""){
        const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`);
        mapboxSearchResults.value =result.data.features;
        // console.log(mapboxSearchResults.value)
        return; 
      }
      mapboxSearchResults.value=null;
    },300)
  }
</script>

