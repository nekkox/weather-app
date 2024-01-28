<script setup>
import { ref, onMounted } from "vue";
const coords = ref();
const geolocationBlockedByUser = ref(false);

const getGeolocation = async () => {
  try {
      // Check if geolocation is blocked by the user
    const position = await new Promise((resolve, reject) => {
      navigator.geolocation.getCurrentPosition(
        (position) => resolve(position),
        (error) => reject(error)
      );
    });
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

<template></template>
