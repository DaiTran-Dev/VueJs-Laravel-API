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
            @click="$emit('click-create', null)"
          >
            Create Task
          </button>
        </div>
      </div>
    </div>
    <b-modal id="modal-create-issue" size="lg" title="Create issue" hide-footer>
      <!-- //Form creat -->
      <CreatTask :taskId="taskId"></CreatTask>
    </b-modal>
  </div>
</template>
<script>
import CreatTask from "./CreateTask.vue";

export default {
  data() {
    return {
      createAnother: false,
    };
  },
  components: {
    CreatTask,
  },
  props: ["title", "taskId"],
};
</script>
<style>
#modal-create-issue .modal-body {
  padding-left: 0;
  padding-right: 0;
}
</style>
