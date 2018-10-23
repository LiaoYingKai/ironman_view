<template>
<div id="app">
  <div class="title">
    好想工作室個人文章累計現況 </br>今天要累積
    <span>{{day}}</span>篇文
  </div>
  <Chart :needPost="day" />
</div>
</template>

<script>
import Chart from './components/Chart'
import moment from 'moment'
export default {
  name: 'App',
  components: {
    Chart
  },
  computed: {
    day: function() {
      var start = moment("20181015")
      var end = moment()
      var diffDays = start.diff(end, 'days')

      return Math.abs(diffDays);
    }
  }
}
</script>

<style>
#app {
  text-align: center;
  font-family: sans-serif;
}

span {
  color: red;
  font-size: 24px;
}
</style>
