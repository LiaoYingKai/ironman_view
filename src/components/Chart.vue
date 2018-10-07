<template>
<div class="chart">
  <ve-bar :data="barChartData"></ve-bar>
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
        rows: []
      },
      contrastName: {
        jasonyangbanana: 'Jason',
        ken09326329: 'Kai',
        soj: 'soj',
        tedlee: 'Ted',
        lai0706: 'Lai',
        andyka1714: 'Andy',
        albert194: 'Albery',
        chris47: 'Chris',
        gg831006: 'Jeremy',
        serendipity: 'Ray',
        mangosu: 'Mango',
        henry97113: 'Henry',
        oklalala: 'TonyLin',
        leiadot: '日安'
      }
    }
  },
  methods: {
    getApi: function() {
      axios.get('http://0.0.0.0:3000/')
        .then(response => {
          response.data.forEach(item => {
            this.barChartData.rows.push({
              'name': this.nameChange(item.name),
              'articlesNumber': item.posts
            })
          })
          console.log(response.data)
        })
        .catch(error => {
          console.log(error)
        })
    },
    nameChange: function(account) {
      let accountArray = account.split("")
      let name = []
      for (let i = (accountArray.indexOf("(") + 1); i < accountArray.indexOf(")"); i++) {
        name.push(accountArray[i])
      }
      name = name.join("")
      return this.contrastName[name]
    }
  },
  mounted: function() {
    this.getApi()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
