<template>
  <b-navbar
    toggleable="lg"
    type="dark"
    variant="dark"
    fixed
    class="p-0 flex-md-nowrap"
    id="header"
  >
    <b-navbar-brand href="#" class="col-md-2 pl-4">
      <div id="logo">
        <b-img fluid src="../assets/devfast-logo.png" alt="Image 1"></b-img>
        <span>Devfast</span>
      </div>
    </b-navbar-brand>
    <b-form-input
      class="w-100 form-control-dark"
      placeholder="Search"
    ></b-form-input>
    <b-navbar-nav class="px-4">
      <b-nav-item class="p-0 text-nowrap" v-if="!$auth.loggedIn"
        ><NuxtLink to="/login" class="btn btn-dark p-0"
          >Sign In</NuxtLink
        ></b-nav-item
      >
      <b-button
        variant="dark"
        v-if="$auth.loggedIn"
        @click="logout()"
        class="p-0 text-nowrap"
        >Sign Out</b-button
      >
    </b-navbar-nav>
  </b-navbar>
</template>

<script>
export default {
  methods: {
    logout() {
      this.$auth.logout();
    },
  },
};
</script>

<style>
#header .navbar-brand {
  font-size: 1rem;
  background-color: rgba(0, 0, 0, 0.25);
  box-shadow: inset -1px 0 0 rgb(0 0 0 / 25%);
  margin-right: 0;
}
#header .form-control:focus {
  border-color: transparent;
  box-shadow: none;
}
.form-control-dark {
  color: #fff;
  background-color: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.1);
  border-radius: 0 !important;
  padding: 1.5rem 1rem;
}
#header .nav-link {
  padding-top: 0;
  padding-bottom: 0;
}
#logo img {
  height: 44px;
}
#logo span {
  font-size: 20px;
}
</style>
