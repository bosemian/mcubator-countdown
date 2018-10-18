<template>
  <div id="app">
    <section id="app" class="hero is-black is-fullheight is-bold">
      <div class="hero-body">
        <div class="container has-text-centered">
          
          <div class="has-text-centered">
              <img class="img-logo" src="../public/logo-mcubator.jpg" alt="mcubator">
          </div>
          
          <div id="timer">
            <span id="minutes">{{ minutes }}</span>
            <span id="middle">:</span>
            <span id="seconds">{{ seconds }}</span>
          </div>

          <div id="buttons">
        <!--     Start TImer -->
            <button 
              id="start" 
              class="button is-primary is-large mr-5" 
              v-if="!timer"
              @click="startTimer">
                <i class="far fa-play-circle"></i>
            </button>
        <!--     Pause Timer -->
            <button 
              id="stop" 
              class="button is-primary is-large mr-5" 
              v-if="timer"
              @click="stopTimer">
                <i class="far fa-pause-circle"></i>
            </button>
        <!--     Restart Timer -->
            <button 
              id="reset" 
              class="button is-primary is-large" 
              v-if="resetButton"
              @click="resetTimer">
                <i class="fas fa-undo"></i>
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'app',

  data () {
    return {
      timer: null,
      totalTime: (3 * 60),
      resetButton: false,
      sound: new Audio(require('../public/mcubator_sound.mp3'))
    }
  },
  methods: {
    startTimer: function() {
      this.playSound()
      this.resetButton = true;
      this.timer = '1'
      setTimeout(() => {
        this.timer = setInterval(() => this.countdown(), 1000);
      }, 7500)
    },
    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
    },
    resetTimer: function() {
      this.totalTime = (3 * 60);
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
    },
    padTime: function(time) {
      return (time < 10 ? '0' : '') + time;
    },
    countdown: function() {
      if(this.totalTime >= 1){
        this.totalTime--;
      } else{
        this.totalTime = 0;
        this.resetTimer()
      }
    },
    playSound () {
      this.sound.play()
    }
  },
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - (this.minutes * 60);
      return this.padTime(seconds);
    }
  }
}
</script>

<style lang="scss">
.img-logo {
  width: 10%;
  height: 20%;
}

.mr-5 {
  margin-right: 20px;
}

#message {
  color: #DDD;
  font-size: 50px;
  margin-bottom: 20px;
}

#timer {
  font-size: 400px;
  line-height: 1;
  margin-bottom: 40px;
}

.is-black {
  background-color: #000 !important;
}
</style>
