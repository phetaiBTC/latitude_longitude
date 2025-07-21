<script setup>
import { ref, onMounted } from 'vue'

const latitude = ref(null)
const longitude = ref(null)
const error = ref('')

onMounted(() => {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      (position) => {
        latitude.value = position.coords.latitude
        longitude.value = position.coords.longitude
      },
      (err) => {
        console.error('Geolocation Error:', err)
        error.value = `Error (${err.code}): ${err.message}`
      }
    )
  } else {
    error.value = 'Geolocation is not supported by this browser.'
  }
})
</script>

<template>
  <div>
    <p v-if="latitude && longitude">
      🌍 Latitude: {{ latitude }}<br />
      🌍 Longitude: {{ longitude }}
    </p>
    <p v-else-if="error">❌ {{ error }}</p>
    <p v-else>📡 กำลังดึงตำแหน่ง...</p>
  </div>
</template>
