<script setup>
import { ref, onMounted } from "vue";

const props = defineProps(["coords"]);
const { latitude, longitude } = props.coords;
const data = ref(null);

const host = "https://api.weatherapi.com/v1/current.json?key=";

async function fetchWeather() {
  const q = `${latitude},${longitude}`;
  const key = import.meta.env.VITE_APP_WEATHER_API_KEY;
  const url = `${host}${key}&q=${q}`;
  console.log(url);

    //Get data from api
  const res = await fetch(url);
  const weatherData = await res.json();
  return weatherData;
}

onMounted(async () => {
  const weatherResponse = await fetchWeather();
  data.value = weatherResponse;
});

console.log("Coords: ", props.coords);
</script>

<template>
  <p>{{ data }}</p>
  {{ console.log(data) }}
</template>
