<template>
  <div class="Favorite">
    <coin-table :coinlist="coinlist" @favorite="unFavorite" buttonbg="bg-gray-500" buttontext="UNFAV">
    <template v-slot="{item}">
      <BaseButton buttonbg="bg-gray-500" buttontext="EDIT" @click="edit(item)"/>
    </template>
    </coin-table>
  </div>
</template>
<script>
import CoinTable from '@/components/CoinTable.vue'
import BaseButton from '@/components/BaseButton.vue'

export default {
  components: {
    CoinTable,
    BaseButton
  },
  async mounted() {
    const { data } = await this.axios.get('http://localhost:5000/cryptolist')
    this.coinlist = await data
  },
  data() {
    return {
      coinlist: []
    }
  },
  methods: {
    async unFavorite(payload) {
      try {
        const res = await this.axios.delete(`http://localhost:5000/cryptolist/${payload.id}`)
        if (res.status === 200) {
          alert(`UNFAVORITED ${payload.name}`)
          const { data } = await this.axios.get('http://localhost:5000/cryptolist')
          this.coinlist = await data
        }

        console.log(res);
      } catch (e) {
        alert(`ERROR`)
      }
    },
    async edit(payload){
      const newName = prompt("Enter New Name","ชื่อใหม่");
      payload.name = newName
      const res = await this.axios.put(`http://localhost:5000/cryptolist/${payload.id}`, payload)
      console.log(res);
    }
  },
}
</script>