<script setup>
import { ref, onMounted } from "vue";
import WindDirection from "./WindDirection.vue";

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
  console.log(weatherResponse);
});

const formatDate = (dateString) => {
  const date = new Date(dateString);
  return new Intl.DateTimeFormat("default", {
    dateStyle: "long",
    timeStyle: "short",
  }).format(date);
};
</script>

<template>
  <div>
    <article
      v-if="data && data.current"
      class="bg-white text-black max-w-md w-96 rounded-lg shadow-lg p-4 flex"
    >
      <div class="text-center basis-1/4">
        <img :src="data.current.condition.icon" class="h-16 w-16" />
      </div>
      <div class="basis-3/4 text-left">
        <h1 class="text-3xl font-bold">
          {{ data.current.condition.text }}
          <span class="text-2xl block">{{ data.current.temp_c }}&#8451;</span>
        </h1>
        <p>{{ data.location.name }} {{ data.location.region }}</p>
        <p>Precipitation: {{ data.current.precip_mm }}mm</p>
        <p>{{ formatDate(data.location.localtime) }}</p>
        <p>
          Wind: {{ data.current.wind_kph }} kph
          <WindDirection :degrees="data.current.wind_degree" />
        </p>
      </div>
    </article>
    <div v-else>Loading...</div>
  </div>
</template>
