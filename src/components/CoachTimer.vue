<template>
  <div class="mt-5">
    <div id="timer">
      <span id="minutes">{{ minutes }}</span>
      <span id="middle">:</span>
      <span id="seconds">{{ seconds }}</span>
    </div>

    <div id="buttons">
      <!--     Start TImer -->
      <button id="start" class="button is-info is-large mr-5" v-if="!timer" @click="startTimer">
        <i class="far fa-play-circle"></i>
      </button>
      <!--     Pause Timer -->
      <button id="stop" class="button is-info is-large mr-5" v-if="timer" @click="stopTimer">
        <i class="far fa-pause-circle"></i>
      </button>
      <!--     Restart Timer -->
      <button id="reset" class="button is-info is-large" v-if="resetButton" @click="resetTimer">
        <i class="fas fa-undo"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CoachTimer",
  data() {
    return {
      timer: null,
      totalTime: 5 * 60,
      resetButton: false,
    };
  },
  methods: {
    startTimer: function() {
      this.timer = setInterval(() => this.countdown(), 1000);
      this.resetButton = true;
    },
    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
    },
    resetTimer: function() {
      this.totalTime = 5 * 60;
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
    },
    padTime: function(time) {
      return (time < 10 ? "0" : "") + time;
    },
    countdown: function() {
      if (this.totalTime >= 1) {
        this.totalTime--;
      } else {
        this.totalTime = 0;
        this.resetTimer();
      }
    }
  },
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - this.minutes * 60;
      return this.padTime(seconds);
    }
  }
};
</script>
<style>
.mt-5 {
  margin-top: 10em;
}
</style>
