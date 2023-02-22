<template>
  <div class="min-h-screen border border-gray-300 border-r max-w-[250px] p-4">
    <div class="flex flex-col text-gray-400">
      <nuxt-link class="py-2 text-center capitalize" :class="{ 'text-blue-500' : $route.path === '/'}" to="/">show</nuxt-link>
      <nuxt-link class="py-2 text-center capitalize" :class="{ 'text-blue-500' : $route.path === '/create'}" to="/create">create</nuxt-link>
      <nuxt-link class="py-2 text-center capitalize" :class="{ 'text-blue-500' : $route.path === '/delete'}" to="/delete">delete</nuxt-link>
      <nuxt-link class="py-2 text-center capitalize" :class="{ 'text-blue-500' : $route.path === '/update'}" to="/update">update</nuxt-link>
    </div>
  </div>
</template>

<script lang="js">
  export default {
    
  }
</script>

<style lang="scss" scoped>

</style>