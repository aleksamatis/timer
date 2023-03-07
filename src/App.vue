<script setup>
import Timer from './components/Timer.vue'
</script>

<template>
  <main>
    <Timer :totalMinutes="5" :totalSeconds="30" />
    <Timer :totalMinutes="10" :totalSeconds="10" />
  </main>
</template>
