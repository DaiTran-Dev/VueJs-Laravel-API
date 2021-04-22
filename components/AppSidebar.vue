<template>
  <b-nav class="flex-column sidebar">
    <b-nav-item><NuxtLink to="/">Categories</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/">Product</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/task/">Task</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/">Dell</NuxtLink></b-nav-item>
  </b-nav>
</template>
<script>
export default {};
</script>

<style>
.sidebar .nuxt-link-active {
  font-weight: 500;
  color: #333;
}
</style>
