<template>
  <div class="scoreboard">
    <table>
      <tr>
        <th colspan="2" style="font-size: 30px">Scoreboard</th>
      </tr>
      <tr
        v-for="(s, i) in score"
        :key="s">
        <td>{{ i + 1 }}</td>
        <td>{{ s }}</td>
      </tr>
    </table>
    <a @click="swapComponent('mainmenu')">
      <i class="fas fa-home"></i>
    </a>
  </div>
</template>

<script>
export default {
  name: 'Scoreboard',
  props: ['swapComponent'],
  data() {
    return {
      scores : []
    }
  },
  created() { this.score = this.$parent.test() || [] }
}
</script>

<style scoped>

  .fas {
    font-size: 70px;
    padding-top: 30px;
  }

  table {
    table-layout: fixed;
    border-radius: 10px;
    border: 1px solid #fff;
    color: #fff;
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    padding: 8px;
    text-align: center;
    border-bottom: 1px solid #ddd;
  }

</style>
