<template>
  <div id="app">
    <section id="app" class="hero is-black is-fullheight is-bold">
      <div class="hero-body">
        <div class="container has-text-centered">
          <div ref="logo" class="fixed" :class="{'is-invisible': hide }">
            <img class="img-s-logo" src="../public/logo-mcubator.jpg" alt="mcubator">
          </div>
          
          <div class="has-text-centered">
            <img class="img-logo" src="../public/logo-mcubator.jpg" alt="mcubator">
          </div>
          
          <competitor-timer></competitor-timer>
          <br>
          <coach-timer></coach-timer>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import CompetitorTimer from './components/CompetitorTimer'
import CoachTimer from './components/CoachTimer'
export default {
  name: 'app',

  data () {
    return {
      hide: true
    }
  },

  components: {
    CompetitorTimer,
    CoachTimer
  }

}
</script>

<style lang="scss">
.img-logo {
  width: 10%;
  height: auto;
}

.fixed {
  position: fixed;
  top: 50px;
  left: 0;
  transition: all .8s;
}

.img-s-logo {
  width: 20%;
  height: auto;
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.28s;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>
