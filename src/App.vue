<template>
  <div id="app">
    <h1 id="title">Countdown Timer</h1>
    <createCounter @counter-created="counterCreated">
    </createCounter>
    <div class="counterText"> 
      <vue-countdown
          v-if="counting"
          :time="countdownTime"
          @end="onCountdownEnd"
          :transform="transformSlotProps"
          v-slot="{hours, minutes, seconds }"
        >
          {{ hours }} hours, {{ minutes }} minutes, {{ seconds }} seconds.
      </vue-countdown>
      <span v-else> 0 hours, 0 minutes, 0 seconds. </span>
    </div>
  </div>
</template>

<script>
import VueCountdown from '@chenfengyuan/vue-countdown';
import createCounter from './components/createCounter.vue';

export default {
  name: 'App',
  components: {
    VueCountdown,
    createCounter
  },
  data() {
    return {
      counting: false,
      countdownTime: 0
    };
  },
  methods: {
    counterCreated(counterObj) {
      const { hours, minutes, seconds } = counterObj;
      const parsedHours = parseInt(hours) || 0;
      const parsedMinutes = parseInt(minutes) || 0;
      const parsedSeconds = parseInt(seconds) || 0;
      this.countdownTime = (parsedHours * 60 * 60 + parsedMinutes * 60 + parsedSeconds) * 1000;
      this.counting = true;
    },
    onCountdownEnd() {
      this.counting = false;
    },
    transformSlotProps({hours, minutes, seconds }) {
      return {hours, minutes, seconds };
    }
  }
}
</script>


<style>
#app {
  font-family: "Anton SC", sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 12vh auto;
}

#title {
  font-size: 4.5rem;
  margin-bottom: 20px;
}

.counterText {
  font-size: 2.5rem;
  margin-top: 20px;
}
</style>
