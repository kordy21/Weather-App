<template>
  <div class="flex font-Roboto flex-col min-h-screen bg-weather-primary">
    <SiteNavigation />
    <RouterView />
  </div>
</template>

<script setup>
  import SiteNavigation from './components/SiteNavigation.vue'
</script>

<style lang="scss" scoped>

</style>