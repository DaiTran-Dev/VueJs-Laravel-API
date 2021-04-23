<template>
  <div>
    <ModalTitleCreateTask
      title="Task"
      :taskId="taskId"
      @click-create="editAction($event)"
    ></ModalTitleCreateTask>
    <div>
      <b-form-input
        v-model="searchText"
        placeholder=" Search Summary... "
        @keyup.enter="searchTask()"
      ></b-form-input>
    </div>
    <ListTaskTable
      class="mt-5"
      :itemsTable="itemsTable"
      @click-edit="editAction($event)"
      @click-delete="deleteAction($event)"
    ></ListTaskTable>
  </div>
</template>
<script>
import constantSystem from "../../constant/constantSystem.vue";
import ModalTitleCreateTask from "../../components/task/ModalTitleCreateTask";
import ListTaskTable from "../../components/task/ListTaskTable.vue";

export default {
  data() {
    return {
      constantSystem: constantSystem,
      itemsTable: [],
      taskId: null,
      searchText: "",
    };
  },
  components: {
    ModalTitleCreateTask,
    ListTaskTable,
  },
  methods: {
    async getAllTask() {
      const response = await this.$axios.$get(this.constantSystem.BASE_API);
      this.itemsTable = response;
    },
    async getTaskBySummary(summary) {
      var url = this.constantSystem.BASE_API + "/summary/like/" + summary;
      const response = await this.$axios.$get(url).then((res) => {
        this.itemsTable = res;
      });
    },
    async deleteTask(id) {
      var url = this.constantSystem.BASE_API + "/" + id;
      const response = await this.$axios.$delete(url);
      this.getAllTask();
    },
    editAction(id) {
      this.taskId = id;
      this.$bvModal.show("modal-create-issue");
    },
    deleteAction(id) {
      if (id != null) {
        this.deleteTask(id);
      }
    },
    searchTask() {
      var summary_search = this.searchText.trim();
      if (summary_search != "") {
        this.getTaskBySummary(summary_search);
      } else {
        this.getAllTask();
      }
    },
  },
  mounted() {
    this.getAllTask();
  },
};
</script>
<style>
</style>
