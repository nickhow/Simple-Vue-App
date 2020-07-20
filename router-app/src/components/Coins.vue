<template>
  <div>
    <p>Name: {{ coin.code }}</p>
    <p>Symbol: {{ coin.symbol }}</p>
    <p>Price (USD): {{ coin.rate }}</p>
  </div>
</template>
<script>
  import axios from 'axios'

  export default {
    name: 'Coins',

    data() {
      return {
        coin: {}
      }
    },

    created() {
      this.fetchData()
    },

    watch: {
      '$route': 'fetchData'
    },

    methods: {
      fetchData() {
        axios.get('https://api.coindesk.com/v1/'+this.$route.params.id+'/currentprice.json')
        .then((resp) => {
          this.coin = resp.data.bpi.USD
          console.log(resp)
        })
        .catch((err) => {
          console.log(err)
        })
      }
    }
  }
</script>