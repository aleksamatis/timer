<template>
  <div class="main">
    timer: {{minutes}}:{{seconds}}.{{milliseconds}}
  </div>
</template>

<script>
  export default {
    props: {
      totalMinutes: {
        type: Number
      },
      totalSeconds: {
        type: Number
      }
  },
  data() {
    return {value: null, interval: null}
  },
  computed: {
    seconds() {
      return (Math.floor(this.value / 1000) % 60).toString().padStart(2, '0')
    },
    minutes() {
      return (Math.floor(this.value / 1000 / 60) % 60).toString().padStart(2, '0')
    },
    milliseconds() {
      return (this.value / 10 % 100).toString().padStart(2, '0')
    }
  },
  mounted() {
      this.value = (this.totalMinutes * 60 + this.totalSeconds) * 1000

      this.interval = setInterval(() => {
        this.value -= 100
        
        if (this.value <= 0) {
          this.value = 0
          clearInterval(interval)
        }
      }, 100)
  },
  beforeUnmount() {
    if (this.interval) {
      clearInterval(this.interval)
    }
  }
}
</script>
