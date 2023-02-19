<template>
  <div class="countdown-timer">
    <div class="countdown-timer__display">
      {{ minutes }}:{{ seconds }}
    </div>
    <div class="countdown-timer__controls">
      <button @click="startTimer" v-if="!timerIsRunning">Start</button>
      <button @click="stopTimer" v-if="timerIsRunning">Stop</button>
      <button @click="resetTimer">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      minutes: 1,
      seconds: '00',
      timerIsRunning: false,
      timer: null,
    };
  },
  methods: {
    startTimer() {
      this.timerIsRunning = true;
      this.timer = setInterval(() => { this.tick(); }, 1000);
    },
    stopTimer() {
      this.timerIsRunning = false;
      clearInterval(this.timer);
    },
    resetTimer() {
      this.stopTimer();
      this.minutes = 1;
      this.seconds = '00';
    },
    tick() {
      if (this.minutes === 0 && this.seconds === '00') {
        this.stopTimer();
      } else if (this.seconds === '00') {
        this.minutes--;
        this.seconds = 59;
      } else {
        this.seconds--;
        if (this.seconds < 10) {
          this.seconds = '0' + this.seconds;
        }
      }
    },
  },
};
</script>

<style>
.countdown-timer {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 2rem;
  margin-top: 2rem;
}

.countdown-timer__display {
  margin-bottom: 1rem;
}

.countdown-timer__controls {
  display: flex;
  gap: 1rem;
}
</style>
