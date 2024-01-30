<script setup>
import { computed } from "vue";
const props = defineProps(["degrees"]);

    //compute css style based on degrees
const windStyle = computed(() => {
  return { transform: "rotate(" + props.degrees + " deg)" };
});
</script>

<template>
  <span>
    <span aria-hidden="true" class="inline-block" :style="windStyle">⬇</span>
    <span class="sr-only">Wind direction: {{ degrees }} degrees</span>
  </span>
</template>
