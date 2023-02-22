<template>
  <div class="text-gray-300 capitalize bg-gray-100 p-2 select-none">
    {{ breadcrumb  }}
  </div>
</template>

<script>
  export default {
    computed: {
      breadcrumb () {
        const routeName = this.$route.path
        return routeName === '/' ? 'Dashboard > Show': `Dashboard > ${routeName.replace('/', '')}`
      }
    }
  }
</script>