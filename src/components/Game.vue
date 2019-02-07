<template>
  <div class="game">
    <div class="numbers">
        <a class="nav" style="float:left" @click="swapComponent('mainmenu')"> <i class="fas fa-home"></i> </a>
        <button class="number">
          {{ next }}
        </button>
        <a class="nav" style="float:right" @click="refresh()"> <i class="fas fa-sync-alt"></i> </a>
        <div id="timer">
          <p
          :class="{'heartBeat animated': over}"
          >{{ time }}</p>
        </div>
      <transition-group name="number">
        <button
          v-if class="number"
          v-for="(num, i) in list"
          :key="num.id"
          @click="num.id == next && !over && time > 0 ? updateCurrent(num.id, i) : incor = 1"
          :class="{'shake animated': incor, 'touched': num.state}"
          @animationend="incor = 0">
          {{ num.id }}
        </button>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Game',
  props: ['swapComponent'],
  data() {
    return {
      over   : false,
      time   : '0.00',
      count  : 26,
      list   : [],
      next   : 1,
      timer  : null,
      incor  : 0,
      saves  : 5,
      tolose : 90
    }
  },
  methods: {
    startTimer() {
      this.next = 1;
      this.time = '0.00';
      this.over = false;
      this.suffle();
      setTimeout(() => {
        let startTime = Date.now();
        this.timer = setInterval(() => {
          let _t = (parseInt(Date.now() - startTime) / 1000).toFixed(2)
          if (_t > 90) {
            clearInterval(this.timer);
            this.time = 'Game over!';
            this.over = true;
          }
          else this.time = _t;
        }, 10);
      }, 1700);
    },
    refresh() {
      clearInterval(this.timer);
      this.createList();
      this.startTimer();
    },
    createList() {
      this.list = [ ...Array(this.count).keys() ].slice(1).map(e => {
        return { 'id' : e, 'state' : false };
      });
    },
    suffle() {
        this.list = this.list.sort(() => { return 0.5 - Math.random() });
    },
    updateCurrent(n, i) {
      let next = n + 1;
      if (next == this.count) {
        clearInterval(this.timer);
        this.over = true;
        this.saveScore();
        setTimeout(() => {
          this.swapComponent('sb');
        }, 2500);
      } else this.next = next;
      this.list[i].state = true;
    },
    saveScore() {
      let scores = localStorage.getItem('score');
      let save = scores ? JSON.parse(scores).sort((a, b) => {return a - b}).slice(0, this.saves-1) : [];
      save.push(this.time);
      localStorage.setItem('score', JSON.stringify(save));
    }
  },
  created() { this.createList() },
  mounted() { this.startTimer() }
}
</script>

<style scoped>

  .nav { padding-top: 5px }

  .number-move {
    transition: transform 1.5s;
  }

  .number:hover {
    background-color: #b5b512;
    color:white;
  }

  button:focus { outline:0 }

  .touched {
  	background-color: #5a5a4a !important;
  	color:white;
  }

  .number {
    margin: 5px;
    border: 0;
    border-radius: 10px;
    background-color: yellow;
    font-size: 30px;
    font-weight: 600;
    height: 50px;
    width: 50px;
    cursor: pointer;
    line-height: 50px;
    text-align: center;
    vertical-align: middle;
  }
  .fas {
    color: #fff;
    font-size: 50px;
  }
</style>
