<template>
  <div id="app">
    <div class="container">
      <div :is="currentComponent" :swap-component="swapComponent"></div>
    </div>
  </div>
</template>

<script>
import MainMenu from './components/MainMenu.vue'
import Game from './components/Game.vue'
import Scoreboard from './components/Scoreboard.vue'

export default {
  name: 'app',
  components: {
    'mainmenu' : MainMenu,
    'game' : Game,
    'sb'   : Scoreboard
  },
  data() {
    return {
      currentComponent : 'mainmenu'
    }
  },
  methods: {
    swapComponent(component) {
      this.currentComponent = component;
    },
    test(a) {
      try {
        let scores = JSON.parse(localStorage.getItem('score'));
        if (typeof scores == 'object') return scores;
      } catch (e) { return false }
    }
  }
}
</script>

<style>

  @import "https://use.fontawesome.com/releases/v5.7.1/css/all.css";
  @import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css";

  body {
    background-color: black;
  }
  .container {
    padding-top: 7%;
    text-align: center;
    width: 300px;
    margin: 0 auto;
  }
  .fas {
    color: #fff;
    font-size: 250px;
    cursor: pointer;
  }
  p, span {
    color: #fff;
    font-size: 40px;
  }
</style>
