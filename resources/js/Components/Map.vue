<template>
    <div class="relative w-full h-full">
      <div id="map" class="z-0"></div>
  
      <!-- Info box floating -->
      <div
        v-if="selectedIncident"
        class="absolute bottom-10 left-10 bg-slate-800/80 text-white rounded-xl p-4 w-80 shadow-xl backdrop-blur-lg"
      >
        <h3 class="text-lg font-semibold mb-2">Info Lokasi</h3>
        <p><span class="font-semibold">Lokasi:</span> {{ selectedIncident.location }}</p>
        <p><span class="font-semibold">Waktu:</span> {{ selectedIncident.time }}</p>
        <p><span class="font-semibold">Status:</span> {{ selectedIncident.status }}</p>
        <button
          class="mt-4 bg-yellow-400 text-black font-semibold px-3 py-1 rounded-full text-sm"
        >
          Lihat Detail
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  import L from 'leaflet'
  import { onMounted, ref } from 'vue'
  
  // Dummy data
  const incidents = [
    {
      id: 1,
      location: 'Jl. Danau Toba No.12, Jember',
      lat: -8.172,
      lng: 113.695,
      time: '10:30 WIB, 25 Oktober 2024',
      status: 'Diproses',
    },
  ]
  
  const selectedIncident = ref(null)
  
  onMounted(() => {
    const map = L.map('map').setView([-8.172, 113.695], 13)
  
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; contributors',
    }).addTo(map)
  
    // Add incident marker
    incidents.forEach((incident) => {
      const circle = L.circle([incident.lat, incident.lng], {
        color: '#00f2ff',
        fillColor: '#00f2ff88',
        fillOpacity: 0.5,
        radius: 500,
      }).addTo(map)
  
      const marker = L.circleMarker([incident.lat, incident.lng], {
        radius: 8,
        fillColor: '#fff',
        fillOpacity: 1,
        color: '#000',
        weight: 2,
      })
        .addTo(map)
        .on('click', () => {
          selectedIncident.value = incident
        })
    })
  })
  </script>
  
  <style scoped>
  #map {
    height: 100%;
  }
  </style>
  