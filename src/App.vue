<script setup>
import {ref} from 'vue'
import Timer from './components/Timer.vue'

const timers = ref([])
const minutes = ref(0)
const seconds = ref(0)

function startTimer() {
  timers.value.push({minutes: minutes.value, seconds: seconds.value})
}
</script>

<template>
  <main>
    <div>
      <input type="number" placeholder="minutes" v-model="minutes" min="0" max="60"/>
      <input type="number" placeholder="seconds" v-model="seconds" min="0" max="50" step="10"/>
      <button @click="startTimer">Start timer</button>
  </div>
    <Timer :totalMinutes="timer.minutes" :totalSeconds="timer.seconds" v-for="timer in timers"/>
  </main>
</template>
