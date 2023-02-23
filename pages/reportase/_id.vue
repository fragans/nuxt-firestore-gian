<template>
  <div class="max-w-md mx-auto p-4">
    <div class="flex flex-col px-4 py-3 shadow-lg">
      <h1 class="text-center text-lg py-2">{{doc.id}}</h1>
      <div class="grid auto-rows-auto gap-3 pb-3">
        <input type="text" v-model="doc.title" placeholder="title">
        <input type="text" v-model="doc.author" placeholder="author">
        <input type="text" v-model="doc.description" placeholder="excerpt">
        <button @click="updatePublished" class="text-white py-2 " :class="[doc.published ? 'bg-blue-300' : 'bg-green-300' ]">
          {{doc.published ? 'published' : 'unpublished'}}
        </button>
      </div>
      <button class="p-3 bg-blue-500 rounded text-white" @click="update">Update</button>
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
    console.log(res.data())
    const resData = res.data()
    resData.id = res.id
    return {
      doc: resData
    }
  },
  methods: {
    update () {
      console.log('update')
    },
    updatePublished () {
      console.log('updatePublished')
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