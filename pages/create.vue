<template>
  <div class="max-w-md mx-auto p-4">
    <div class="flex flex-col px-4 py-3 shadow-lg">
      <h1 class="text-center text-lg">Insert</h1>
      <div class="grid auto-rows-auto gap-3 pb-3">
        <input type="text" v-model="slug" placeholder="slug">
        <input type="text" v-model="title" placeholder="title">
        <input type="text" v-model="author" placeholder="author">
        <input type="text" v-model="excerpt" placeholder="excerpt">
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
          url: 'https://d3w4qaq4xm1ncv.cloudfront.net/pilihanku/pilihanku-empty-state.png',
          width: 500,
          height: 200
        },
        published: false
      }
    },
    methods: {
      async insert () {
        try {
          console.log('insert')
          const insertRef = this.$fire.firestore.collection("reportase_langsung").doc(this.slug)
          await insertRef.set({
            author: this.author,
            slug: this.slug,
            title: this.title,
            description: this.excerpt,
            thumbnail: this.thumbnail,
            published: false
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