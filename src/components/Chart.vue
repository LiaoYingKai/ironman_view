<template>
<div class="chart">
  <ve-bar :data="barChartData" :judge-width="true" height="800px"></ve-bar>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'chart',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      barChartData: {
        columns: ['name', 'articlesNumber'],
        rows: [],
        height: '800px'
      },
    }
  },
  methods: {
    getApi: function() {
      axios.get('https://protected-savannah-47772.herokuapp.com/')
        .then(response => {
          response.data.forEach(item => {
            this.barChartData.rows.push({
              'name': item.name,
              'articlesNumber': item.posts
            })
          })
          console.log(response.data)
          console.log(this.barChartData.rows)
        })
        .catch(error => {
          console.log(error)
        })
    },
  },
  mounted: function() {
    this.getApi()
  }
}
</script>

<style scoped lang="scss">
h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
