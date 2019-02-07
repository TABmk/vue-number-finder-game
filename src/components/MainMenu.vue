<template>
  <div class="mainmenu">
    <p>An vue-number-finder-game</p>
      <i @click="swapComponent('game')" class="fas fa-play-circle"></i>
      <i @click="swapComponent('sb')" class="second fas fa-list-ol"></i>
      <a href="http://github.com/tabmk/vue-number-finder-game"><i class="second fab fa-github"></i></a>
    <p>Best score: {{ score }}</p>
  </div>
</template>

<script>
export default {
  name: 'MainMenu',
  props: ['swapComponent'],
  data() {
    return {
      score : '0.00'
    }
  },
  created() { this.score = this.$parent.test()[0] || '0.00' }
}
</script>

<style scoped>

  .buttons { display: inline-grid }

  .second {
    color: #fff;
    font-size: 70px;
    padding-top: 20px;
    margin: 5px;
  }

</style>
