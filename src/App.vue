<script setup>
  import SearchInput from './components/SearchInput.vue'
  import { ref } from 'vue'
  import WeatherCard from './components/WeatherCard.vue';


  const places = ref([])

  const addPlace = (data) => {
    places.value.push(data)
  }

  const deletePlace = (name) => {
    // console.log(name)
    if(confirm('Are you sure? ')){
      places.value = places.value.filter((p) => p.location.name !== name)
    }
    
  }

</script>

<template>
  <main>

     <!-- Date -->
      <div class="text-center mb-6">
        {{ new Date().toLocaleDateString('en-us',{
            weekday: 'long',
            year: 'numeric',
            month: 'long',
            day: 'numeric'
        }) }}
      </div>

       <!-- Search -->
       <div>
          <SearchInput @place-data="addPlace"/>
       </div>

       <!-- Weather cards -->
       <div class="grid gap-4 lg:grid-cols-2 md:grid-cols-2 sm:grid-cols-1">
        <div v-for="(place, index) in places" :key="index">
          <WeatherCard 
            :place="place"
            @delete-place="deletePlace" />
        </div>
       </div>
       
  </main>
</template>