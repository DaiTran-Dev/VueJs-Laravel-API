<template>
  <b-nav class="flex-column sidebar">
    <b-nav-item><NuxtLink to="/task/" v-if="$auth.loggedIn">Task</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/" v-if="$auth.loggedIn">Product</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/task/" v-if="$auth.loggedIn">Category</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/" v-if="$auth.loggedIn">Blog</NuxtLink></b-nav-item>
    <b-nav-item><NuxtLink to="/task/" v-if="$auth.loggedIn">Message</NuxtLink></b-nav-item>
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
