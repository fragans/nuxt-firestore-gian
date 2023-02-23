<template>
  <div>
    <nav class="px-4 py-3 flex items-center gap-4">
      <button @click="$router.app.refresh()" class="text-white rounded bg-blue-300 px-3 py-2" name="published">
        <span>All</span>
      </button>
      
      <button @click="filter('published')" class="text-white rounded bg-blue-300 px-3 py-2" name="published">
        <span>isPublished</span>
      </button>
    </nav>
    <div class="w-full text-gray-300 px-4 text-right"> {{ docs.length }} reportase ditemukan </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-x-3 gap-y-4 py-4 px-3 rounded">
      
      <div v-for="(doc, key) in docs" :key="key">
        <card :item="doc"></card>
      </div>
    </div>
  </div>
  
</template>

<script lang="js">
export default {
  async asyncData({$fire}){
    // fetch 1 document
    const docRef = $fire.firestore.collection('reportase_langsung')
    const res = await docRef.get()
    const docs = []
    res.forEach(item => {
      const doc = item.data()
      doc.id = item.id
      docs.push(doc)
    });
    return {
      docs,
      activeFilter: []
    }

  },
  methods: {
    async filter (key) {
      this.activeFilter.push(key)
      const docRef = this.$fire.firestore.collection('reportase_langsung')
      const res = await docRef.where("published", "==", true).get()
      const docs = []
      res.forEach(item => {
        const doc = item.data()
        doc.id = item.id
        docs.push(doc)
      })
      this.docs = docs
    }
  }
}
</script>

<style lang="postcss" scoped>
button {
  @apply hover:bg-blue-200
}
</style>