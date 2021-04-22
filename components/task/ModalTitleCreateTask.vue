<template>
  <div>
    <div
      class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center mt-5 pb-2 mb-3 border-bottom"
    >
      <h1 class="h2">{{ title }}</h1>
      <div class="btn-toolbar mb-2 mb-md-0">
        <div class="btn-group mr-2">
          <button
            class="btn btn-lg btn-outline-secondary"
            v-b-modal.modal-create-issue
          >
            Create Task
          </button>
        </div>
      </div>
    </div>
    <b-modal id="modal-create-issue" size="lg" title="Create issue" hide-footer>
      <!-- //Form creat -->
      <CreatTask :activeCreate="activeCreate"></CreatTask>
      <div class="footer-modal d-flex justify-content-end">
        <b-form-checkbox
          v-model="createAnother"
          name="createAnother"
          value="true"
          unchecked-value="false"
          class="mr-4"
        >
          <span class="text-nowrap">Create Another</span>
        </b-form-checkbox>
        <b-button variant="primary" class="mr-3" size="sm" @click="createTask()"
          >Create</b-button
        >
        <b-button size="sm">Cancel</b-button>
      </div>
    </b-modal>
  </div>
</template>
<script>
import CreatTask from "./CreateTask.vue";

export default {
  data() {
    return {
      createAnother: false,
      activeCreate: false,
    };
  },
  components: {
    CreatTask,
  },
  props: ["title"],
  methods: {
    createTask() {
      this.activeCreate = true;
    },
  },
};
</script>
<style>
.footer-modal {
  border-top: 1px solid #dee2e6;
  padding-top: 20px;
  margin-top: 20px;
}
</style>
