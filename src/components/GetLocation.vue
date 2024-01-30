<script setup>
import WeatherReport from "./WeatherReport.vue";

import { ref, onMounted } from "vue";
const coords = ref();
const geolocationBlockedByUser = ref(false);

const getGeolocation = async () => {
  try {
    // Check if geolocation is blocked by the user
    const position = await new Promise((resolve, reject) => {
      navigator.geolocation.getCurrentPosition(
        function (position) {
          resolve(position);
        },
        function (error) {
          reject(error);
        }
      );
    });
    console.log(position);

    // If geolocation is not blocked, get the coordinates
    coords.value = {
      latitude: position.coords.latitude,
      longitude: position.coords.longitude,
    };
    return "working";
  } catch (error) {
    geolocationBlockedByUser.value = true;
    console.error("Error getting geolocation:", error);
    return "error";
  }
};

onMounted(async () => {
  const getLocation = await getGeolocation();
  console.log(getLocation);
});
</script>

<template>
  <div v-if="coords && !geolocationBlockedByUser" :coords="coords">
    <WeatherReport :coords="coords" />
  </div>
  <div v-if="geolocationBlockedByUser">User denied access</div>
</template>
