<template>
  <div class="stopwatch">
    <h1>Stopwatch</h1>
    <div class="time">{{ formattedTime }}</div>
    <div class="controls">
      <button @click="startStopwatch">Start</button>
      <button @click="stopStopwatch">Stop</button>
      <button @click="resetStopwatch">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      time: 0,
      timer: null,
    };
  },
  computed: {
    formattedTime() {
      const minutes = String(Math.floor(this.time / 60000)).padStart(2, '0');
      const seconds = String(Math.floor((this.time % 60000) / 1000)).padStart(2, '0');
      const milliseconds = String(this.time % 1000).padStart(3, '0');
      return `${minutes}:${seconds}:${milliseconds}`;
    },
  },
  methods: {
    startStopwatch() {
      if (!this.timer) {
        this.timer = setInterval(() => {
          this.time += 10;
        }, 10);
      }
    },
    stopStopwatch() {
      clearInterval(this.timer);
      this.timer = null;
    },
    resetStopwatch() {
      this.stopStopwatch();
      this.time = 0;
    },
  },
};
</script>

<style scoped>
.stopwatch {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
  font-family: Arial, sans-serif;
}
.time {
  font-size: 48px;
  margin: 20px 0;
}
.controls button {
  margin: 0 10px;
  padding: 10px 20px;
  font-size: 16px;
}
</style>
