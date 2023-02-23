<template>
  <nuxt-link :to="`/reportase/${item.id}`">
    <div class="shadow-lg rounded-b-lg">
      <div class="bg-center bg-cover bg-gray-100" :style="thumbnail"></div>
      <div class="px-3 py-2 text-gray-700">
        <h3 class="text-lg font-bold capitalize">{{item.title}}</h3>
        <div class="flex justify-between items-center">
          <span class="text-gray-400 text-sm">Oleh: {{  item.author }}</span>
          <!-- <time class="text-xs">{{ new Date(item.published_date.seconds * 1000).toLocaleString() }}</time> -->
        </div>

        <p class="text-gray-500 text-sm">{{ item.description }}</p>
        
      </div>
    </div>
  </nuxt-link>
  
</template>

<script lang="js">
  export default {
    props: ['item'],
    computed: {
      thumbnail () {
        return {
          backgroundImage: `url(${this.item.thumbnail.url})`,
          paddingBottom: `${56.25}%`
        }
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>