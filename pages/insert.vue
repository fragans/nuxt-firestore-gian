<template>
  <div class="max-w-md mx-auto p-4">
    <div class="flex flex-col px-4 py-3 shadow-lg">
      <h1 class="text-center text-lg py-2 font-bold">Insert</h1>
      <div class="grid auto-rows-auto gap-3 pb-3 text-gray-700">
        <input type="text" v-model="slug" placeholder="slug">
        <input type="text" v-model="title" placeholder="title">
        <input type="text" v-model="author" placeholder="author">
        <input type="text" v-model="excerpt" placeholder="excerpt">
        <input type="text" v-model="thumbnail.url" placeholder="thumbnail">
        <div class="bg-center bg-cover bg-gray-100" :style="[{backgroundImage:`url(${thumbnail.url})`, paddingBottom: '56.25%'}]"></div>
      </div>
      <button class="p-3 bg-blue-500 rounded text-white" @click="insert">Add</button>
    </div>
    
  </div>
</template>

<script lang="js">
  export default {
    data() {
      return { 
        slug: 'bom_bali_2010',
        title: 'bom bali 2010',
        excerpt: 'ada bom meledak di bali denpasar',
        author: 'anton',
        thumbnail: {
          url: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT_YCalozv20Oki516pDRvDiNfByLm_OxvEZc6_XN6TIw&s',
          width: 500,
          height: 200
        },
        published: false
      }
    },
    methods: {
      async insert () {
        try {
          const insertRef = this.$fire.firestore.collection("reportase_langsung").doc(this.slug)
          await insertRef.set({
            author: this.author,
            title: this.title,
            description: this.excerpt,
            thumbnail: this.thumbnail,
            published: false,
            published_date_timestamp: parseInt((new Date().getTime() / 1000 ).toFixed(0)),
            thumbnail: {
              url: this.thumbnail.url,
              width: 200,
              height: 500
            }
          })
          this.$router.push('/')
        } catch (err) {
          console.error(err)
        }
        

      }
    }
  }
</script>

<style lang="postcss" scoped>
input {
  @apply p-2;
  @apply rounded;
  @apply bg-gray-100;
}
</style>