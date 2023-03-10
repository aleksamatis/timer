<template>
  <span class="main">
    <span v-if="targetTime">
      {{minutes}}:{{seconds}}.{{milliseconds}}
    </span>
    <span v-if="value === 0 && targetTime">
      - {{ targetTime.format('H:mm:ss') }}
    </span>
  </span>
</template>

<script>
  import moment from 'moment'
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
      return {
        targetTime: null,
        value: null
      }
    },
    computed: {
      seconds() {
        return (Math.floor(this.value / 1000) % 60).toString().padStart(2, '0')
      },
      minutes() {
        return (Math.floor(this.value / 1000 / 60) % 60).toString().padStart(2, '0')
      },
      milliseconds() {
        return (Math.floor(this.value / 10) % 100).toString().padStart(2, '0')
      },
    },
    mounted() {
      const now = moment()
      this.targetTime = now.add(this.totalMinutes, 'minutes').add(this.totalSeconds, 'seconds')

      this.interval = setInterval(() => {
        this.value = this.targetTime - moment()

        if (this.value <= 0) {
          this.value = 0
          clearInterval(interval)
        }
      }, 10)
    },
    beforeUnmount() {
      if (this.interval) {
        clearInterval(this.interval)
      }
    }
  }
</script>