<template>
  <div>
    <div id="timer">
      <span id="minutes">{{ minutes }}</span>
      <span id="middle">:</span>
      <span id="seconds">{{ seconds }}</span>
    </div>
    <div id="buttons">
      <!--     Start TImer -->
      <button id="start" class="button is-primary is-large mr-5" v-if="!timer" @click="startTimer">
        <i class="far fa-play-circle"></i>
      </button>
      <!--     Pause Timer -->
      <button id="stop" class="button is-primary is-large mr-5" v-if="timer" @click="stopTimer">
        <i class="far fa-pause-circle"></i>
      </button>
      <!--     Restart Timer -->
      <button id="reset" class="button is-primary is-large" v-if="resetButton" @click="resetTimer">
        <i class="fas fa-undo"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CompetitorTimer",
  data() {
    return {
      timer: null,
      totalTime: 5 * 60,
      resetButton: false,
      sound: new Audio(require("../../public/mcubator_sound.mp3"))
    };
  },
  methods: {
    startTimer: function() {
      this.playSound()
      this.resetButton = true
      this.timer = "1"
      setTimeout(() => {
        this.timer = setInterval(() => this.countdown(), 1000)
      }, 7000)
    },
    stopTimer: function() {
      clearInterval(this.timer)
      this.timer = null
      this.resetButton = true
    },
    resetTimer: function() {
      this.totalTime = 5 * 60
      clearInterval(this.timer)
      this.timer = null
      this.resetButton = false
    },
    padTime: function(time) {
      return (time < 10 ? "0" : "") + time
    },
    countdown: function() {
      if (this.totalTime >= 1) {
        this.totalTime--
      } else {
        this.totalTime = 0
        this.resetTimer()
      }
    },
    playSound() {
      this.sound.play()
    }
  },
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60)
      return this.padTime(minutes)
    },
    seconds: function() {
      const seconds = this.totalTime - this.minutes * 60
      return this.padTime(seconds)
    }
  }
}
</script>
