<template>
    <div class="container mx-auto">
        <table class="w-full table-auto">
          <thead class="justify-between">
            <tr class="bg-gray-800">
              <th class="px-10 py-2">
                <span class="text-gray-300"></span>
              </th>
              <th class="px-10 py-2">
                <span class="text-gray-300"></span>
              </th>
              <th class="px-10 py-2">
                <span class="text-gray-300"></span>
              </th>
              <th class="px-2 py-2">
                <span class="text-gray-300">Name</span>
              </th>
              <th class="px-2 py-2 text-right">
                <span class="text-gray-300">Price</span>
              </th>
              <th class="px-2 py-2 text-right">
                <span class="text-gray-300">24h %</span>
              </th>
              <th class="px-2 py-2 text-right">
                <span class="text-gray-300">7d %</span>
              </th>
    
              <th class="px-2 py-2 text-right">
                <span class="text-gray-300">Market Cap</span>
              </th>
    
              <th class="px-2 py-2 text-right pr-10">
                <span class="text-gray-300">Volume</span>
              </th>
            </tr>
          </thead>
          <tbody class="bg-gray-200">
            <tr v-for="item in coinlist" :key="item.id" class="bg-white border-4 border-gray-200">
              <td class="px-10 py-2 flex flex-row items-center">
                <img
                  class="h-8 w-8 rounded-full object-cover "
                  :src="`https://cryptoicon-api.vercel.app/api/icon/${item.symbol.toLowerCase()}`"
                  alt=""
                />
              </td>
              <td class="text-right px-2 py-2 font-bold">
                <BaseButton :buttonbg="buttonbg" :buttontext="buttontext" @click="favorite(item)"/>
              </td>
              <td class="text-left">
              <slot :item="item">
              </slot>
              </td>
              <td>
                <span class="text-center ml-2 font-semibold">{{ item.name }} <span class="text-gray-400">{{item.symbol}}</span></span>
                
              </td>
              <td class="text-right px-2 py-2 font-bold">
                <span>${{item.quote.USD.price.toFixed(2)}}</span>
              </td>
              <td class="text-right px-2 py-2">
                <span>{{item.quote.USD.percent_change_24h.toFixed(2)}}%</span>
              </td>
              <td class="text-right px-2 py-2">
                <span>{{item.quote.USD.percent_change_7d.toFixed(2)}}%</span>
              </td>
              <td class="text-right px-2 py-2">
                <span>{{item.quote.USD.market_cap.toFixed(2)}}</span>
              </td>
    
              <td class="px-2 py-2 text-right pr-10">
                <span>
                  {{item.quote.USD.volume_24h.toFixed(2)}}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
</template>

<script>
import BaseButton from './BaseButton.vue'

export default {
    components : {
      BaseButton
    },
    props : [
        "coinlist",
        "buttonbg",
        "buttontext"
    ],
    methods : {
      favorite(payload){
        this.$emit("favorite",payload)
      }
    }
}
</script>