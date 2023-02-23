<template>
  <div class="min-h-screen border border-gray-200 border-r min-w-[150px] p-4">
    <div class="flex flex-col text-gray-400 gap-2 ">
      <nuxt-link class="py-2 capitalize hover:bg-gray-100 w-full px-3 rounded-lg" to="/">show</nuxt-link>
      <nuxt-link class="py-2 capitalize hover:bg-gray-100 w-full px-3 rounded-lg" to="/create">create</nuxt-link>
      <nuxt-link class="py-2 capitalize hover:bg-gray-100 w-full px-3 rounded-lg" to="/delete">delete</nuxt-link>
      <nuxt-link class="py-2 capitalize hover:bg-gray-100 w-full px-3 rounded-lg" to="/update">update</nuxt-link>
    </div>
  </div>
</template>

<script lang="js">
  export default {
    
  }
</script>

<style lang="postcss" scoped>
  .nuxt-link-exact-active {
    @apply font-bold;
    @apply text-blue-500;
  }
</style>