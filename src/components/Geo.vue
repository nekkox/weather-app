<script setup>
import { ref, onMounted } from "vue";

const coords = ref();
//walk the dog then
//make the dog food then
//go watch tv then
// go play dota then go to sleep. END

async function walkTheDog() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("walked the dog");
      // console.log('walked the dog - ok')
    }, 2000);
  });
}

async function makeTheDogFood() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("food");
      // console.log('make the dog food - ok')
    }, 2000);
  });
}

async function watchTv() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("watch tv");
      // console.log('watch tv - ok')
    }, 2000);
  });
}

onMounted(async () => {
  try {
    const walk = await walkTheDog().then((res) => console.log(res));
    const food = await makeTheDogFood();
    const tv = await watchTv();
    console.log("ok");
  } catch (err) {
    console.log(err);
  }
});
</script>
<template></template>

// Call the getCoords function getCoords();
