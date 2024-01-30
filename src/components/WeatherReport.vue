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
  console.log("q", q);

  //Get data from api
  try {
    const res = await fetch(url);
    const weatherData = await res.json();
    return weatherData;
  } catch (err) {
    console.log("sorry, data not fetched");
  }
}

onMounted(async () => {
  const { latitude, longitude } = props.coords;
  const weatherResponse = await fetchWeather();
  data.value = weatherResponse;
});
</script>

<template>
  <div>
    <article v-if="data && data.current">
      <p>Data:</p>
      {{ data.current }}
    </article>
    <div v-else>Loading...</div>
  </div>
</template>
