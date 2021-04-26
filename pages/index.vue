<template>
  <div class="container mt-5">
    <h1 v-if="$auth.loggedIn">Hello {{ user.name }}</h1>
    <h1 v-if="!$auth.loggedIn">Please sign in</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: null,
    };
  },
  created() {
    this.user = this.$auth.user;
    console.log(this.$auth);
  },
};
</script>
