<template>
  <div class="stopwatch-widget">
    <div class="widget-content">
      <h2>Stopwatch</h2>
      <p>{{ formatTime }}</p>
      <div>
        <button @click="toggleStopwatch" :class="{ 'stop': isRunning, 'start': !isRunning }">
          {{ isRunning ? 'Pause' : 'Start' }}
        </button>
        <button @click="resetStopwatch">Reset</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
    };
  },
  computed: {
    formatTime() {
      const milliseconds = this.elapsedTime % 1000;
      const seconds = Math.floor(this.elapsedTime / 1000) % 60;
      const minutes = Math.floor(this.elapsedTime / 60000) % 60;
      const hours = Math.floor(this.elapsedTime / 3600000);

      return `${hours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${milliseconds.toString().padStart(3, '0')}`;
    },
  },
  methods: {
    toggleStopwatch() {
      if (this.isRunning) {
        this.stopStopwatch();
      } else {
        this.startStopwatch();
      }
    },
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now();

        this.timerInterval = setInterval(() => {
          const currentTime = Date.now();
          const elapsedTimeSinceStart = currentTime - this.startTime;
          this.elapsedTime += elapsedTimeSinceStart;
          this.startTime = currentTime;
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      clearInterval(this.timerInterval);
      this.elapsedTime = 0;
    },
  },
};
</script>

<style scoped>
.stopwatch-widget {
  display: flex;
  justify-content: center;
}

.stopwatch-widget .widget-content {
  text-align: center;
}

.stopwatch-widget h2 {
  color: #333;
  font-size: 30px;
  margin-top: 50px;
  margin-bottom: 50px;
}

.stopwatch-widget p {
  color: #333;
  font-size: 55px;
  margin-bottom: 55px;
  align-items: center;
}

.stopwatch-widget button {
  margin-right: 13px;
  padding: 15px 25px;
  background: rgb(252, 50, 50);
  color: white;
  border: none;
  border-radius: 15px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-weight: bold;
}

.stopwatch-widget button.start {
  background-color: #4caf50;
}

.stopwatch-widget button.start:hover {
  background-color: #347938;
}

.stopwatch-widget button.stop:hover {
  background-color: #45a049;
}

.stopwatch-widget button:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}
</style>