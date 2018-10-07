<template>
<div id="app">
  <div class="title">
    好想工作室個人文章累計現況 </br>今天要累積
    <span>{{day-1}}</span>篇文
  </div>
  <Chart/>
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
      let day = moment("20181015", "YYYYMMDD").fromNow().split("")
      let todayPostNumber = []
      todayPostNumber.push(day[0], day[1])
      return todayPostNumber.join('');
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
