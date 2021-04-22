<template>
  <div>
    <AppHeader></AppHeader>
    <b-container fluid>
      <b-row>
        <!-- Start Sidebar  -->
        <b-col md="2">
          <AppSidebar></AppSidebar>
        </b-col>
        <!-- End sidebar -->
        <!-- Start Content page -->
        <b-col md="10" class="pl-0">
          <Nuxt/>
        </b-col>
        <!-- End Content page -->
      </b-row>
    </b-container>
  </div>
</template>
<script>
import AppHeader from "../components/AppHeader.vue";
import AppSidebar from "../components/AppSidebar.vue";
export default {
  components: {
    AppHeader,
    AppSidebar,
  },
};
</script>
