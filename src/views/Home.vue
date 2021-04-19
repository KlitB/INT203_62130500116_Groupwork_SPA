<template>
  <div class="home">
    <coin-table :coinlist="coinlist" @favorite="favorite" buttonbg="bg-yellow-500" buttontext="FAV"/>
  </div>
</template>

<script>

import CoinTable from '@/components/CoinTable.vue'

export default {
  name: 'Home',
  components: {
    CoinTable
  },
  async mounted() {
    const { data } = await this.axios.get('http://localhost:5000/coinmarket')
    this.coinlist = await data
  },
  data() {
    return {
      coinlist: []
    }
  },
  methods: {
    async favorite(payload) {
      try {
        const res = await this.axios.post('http://localhost:5000/cryptolist', payload)
        if (res.status === 201) {
          alert(`FAVORITED ${payload.name}`)
        }
        console.log(res);
      }catch (e) {
        alert(`Already added`)
      }
  }
  },
}
</script>