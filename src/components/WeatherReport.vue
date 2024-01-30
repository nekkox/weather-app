<script setup>
    import { ref, onMounted, defineProps } from "vue";

    const { coords } = defineProps(['coords']);

    const data = ref(null);
console.log(import.meta.env)
    
    const host = 'https://api.weatherapi.com/v1/current.json?key=';

    const fetchWeather = async (coords) => {
        const { latitude, longitude } = coords;
        const q = `${latitude},${longitude}`;
        const url = `${host}${key}&q=${q}`;

        try {
            const res = await fetch(url);
            const weatherData = await res.json();
            //console.log(weatherData)
            return weatherData;
        } catch (error) {
            console.error('Error fetching weather:', error);
            return null;
        }
    }

    onMounted(async () => {
        try {
            const weatherResponse = await fetchWeather(coords);
            data.value = weatherResponse;
            
        } catch (error) {
            console.error('Error setting weather data:', error);
        }
    });
</script>


<template></template>
