<template>
  <main>
    <!-- date -->
    <div class="text-center mb-6">
      {{
        new Date().toLocaleDateString('en-us', {
          weekday: 'long',
          month: 'long',
          year: 'numeric',
          day: 'numeric',
        })
      }}
    </div>
    <!-- search -->
    <div>
      <searchInput @place-data="AddPlace" />
    </div>

    <!-- Weather card -->
    <div class="grid grid-cols-3 gap-4">
      <div v-for="(place, idx) in places" :key="idx">
        <weatherCard :place="place" @delete-place="DeletePlace" />
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue'
import searchInput from './components/searchInput.vue'
import weatherCard from './components/weatherCard.vue'

const places = ref([])
const AddPlace = (data) => {
  // console.log(data)

  places.value.push(data)
}
const DeletePlace = (name) => {
  if (confirm('Are you sure')) {
    places.value = places.value.filter((p) => p.location.name !== name)
  }
}
</script>