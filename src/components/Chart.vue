<template>
<div class="chart">
  <ve-bar :data="chartData" :judge-width="true" height="800px" :extend="chartExtend" :loading="!chartData.rows.length"></ve-bar>
</div>
</template>

<script>
import axios from 'axios';
import moment from 'moment'
import 'v-charts/lib/style.css'

var post = this.needPost
export default {
  name: 'chart',
  props: ['needPost'],
  data() {
    this.chartExtend = {
      series(s) {
        s[0].data = s[0].data.map(item => {
          if (item < day()) {
            return {
              value: parseInt(item),
              itemStyle: {
                color: 'red'
              }
            }
          } else {
            if (item == 30) {
              return {
                value: parseInt(item),
                itemStyle: {
                  opacity: 0,
                },
              }
            } else {
              return {
                value: parseInt(item),
                itemStyle: {
                  color: '#8bc34a',
                  opacity: 0.25,
                }
              }
            }
          }
        })
        console.log('> ', s)

        function day() {
          let day = moment("20181015", "YYYYMMDD").fromNow().split("")
          let todayPostNumber = []
          todayPostNumber.push(day[0], day[1])
          return (parseInt(todayPostNumber.join('')) - 1);
        }
        return s
      }
    }
    return {
      chartData: {
        columns: ['name', 'posts'],
        rows: [],
      },
    }
  },
  created: function() {
    axios.get('https://protected-savannah-47772.herokuapp.com/')
      .then(response => {
        this.chartData.rows = response.data.map(item => ({
          name: item.name,
          posts: item.posts
        }))
        this.chartData.rows.sort(function(a, b) {
          console.log(">", a)
          console.log(">>>>>", b)
          return b.posts - a.posts
        })
        this.chartData.rows.push({
          name: "參賽者",
          posts: 30
        })
      })
      .catch(error => {
        console.log(error)
      })
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
