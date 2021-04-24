<template>
  <b-navbar
    toggleable="lg"
    type="dark"
    variant="dark"
    fixed
    class="p-0 flex-md-nowrap"
    id="header"
  >
    <b-navbar-brand href="#" class="col-md-2">Company name</b-navbar-brand>
    <b-form-input
      class="w-100 form-control-dark"
      placeholder="Search"
    ></b-form-input>
    <b-navbar-nav class="px-4">
      <b-nav-item href="#" class="p-0 text-nowrap">Sign out</b-nav-item>
    </b-navbar-nav>
  </b-navbar>
</template>

<script>
export default {};
</script>

<style>
#header .navbar-brand {
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  font-size: 1rem;
  background-color: rgba(0, 0, 0, 0.25);
  box-shadow: inset -1px 0 0 rgb(0 0 0 / 25%);
  margin-right: 0;
}
#header .form-control:focus {
  border-color: transparent;
  box-shadow:none;
}
.form-control-dark {
  color: #fff;
  background-color: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.1);
  border-radius: 0 !important;
  padding: 1.3rem 1rem;
}
#header .nav-link {
  padding-top: 0;
  padding-bottom: 0;
}
</style>
