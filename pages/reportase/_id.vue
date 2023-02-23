<template>
  <div class="max-w-md mx-auto p-4">
    <div class="flex flex-col px-4 py-3 rounded-lg shadow-lg">
      <h1 class="text-center text-lg py-2 font-bold text-gray-400">{{doc.id}}</h1>
      <div class="grid auto-rows-auto gap-3 pb-3">
        <button
          @click="updatePublished"
          class="text-white py-2 "
          :class="[doc.published ? 'bg-blue-300' : 'bg-red-300' ]"
        >
          {{doc.published ? 'published' : 'unpublished'}}
        </button>
        <input type="text" v-model="doc.title" placeholder="title">
        <input type="text" v-model="doc.author" placeholder="author">
        <input type="text" v-model="doc.description" placeholder="excerpt">
        <input type="text" :placeholder="`${doc.published_date_timestamp} (UNIX)`" disabled>
        <input type="text" v-model="doc.thumbnail.url" placeholder="thumbnail">
        
      </div>
      <div class="grid grid-cols-2 gap-4">
        <button class="p-3 bg-blue-500 rounded text-white" @click="update">Update</button>
        <button class="p-3 bg-red-400 rounded text-white" @click="deleteDoc">Delete</button>
      </div>
      
    </div>
    
  </div>
</template>

<script lang="js">

export default {
  async asyncData({$fire, params}){
    // fetch 1 document
    const { id } = params
    const docRef = $fire.firestore.collection('reportase_langsung').doc(id)
    const res = await docRef.get()
    const resData = res.data()
    resData.id = res.id
    return {
      doc: resData
    }
  },
  methods: {
    async deleteDoc () {
      const docRef = this.$fire.firestore.collection("reportase_langsung").doc(this.$route.params.id)
      await docRef.delete()
      this.$router.push('/')
    },
    async update () {
      console.log('update', this.$route.params.id)
      try {
        const docRef = this.$fire.firestore.collection('reportase_langsung').doc(this.$route.params.id)
        await docRef.update(
          {
            title: this.doc.title,
            author: this.doc.author,
            description: this.doc.description,
            thumbnail: {
              width: this.doc.thumbnail.width,
              height: this.doc.thumbnail.height,
              url: this.doc.thumbnail.url
            }
          }
        )
        this.$router.push('/')
      } catch (error) {
        console.error('update err:', error)
      }
    },
    async updatePublished () {
      console.log('updatePublished', this.$route.params.id)
      try {
        const docRef = this.$fire.firestore.collection('reportase_langsung').doc(this.$route.params.id)
        await docRef.update(
          {
            published: !this.doc.published
          }
        )
        console.log('updatePublished')
        this.$router.push('/')
      } catch (error) {
        console.error('updatePublished err:', error)
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