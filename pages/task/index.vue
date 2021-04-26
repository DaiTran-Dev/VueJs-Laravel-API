<template>
  <div v-if="itemsTable.length > 0">
    <ModalTitleCreateTask
      title="Task"
      :taskId="taskId"
      @click-create="editAction($event)"
      @load-table="getAllTask()"
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
  <div v-else>
    <h1>Ko co data</h1>
  </div>
</template>

<script>
import ModalTitleCreateTask from "../../components/task/ModalTitleCreateTask";
import ListTaskTable from "../../components/task/ListTaskTable.vue";

export default {
  data() {
    return {
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
      const response = await this.$axios.$get("tasks");
      this.itemsTable = response;
    },
    async getTaskBySummary(summary) {
      const response = await this.$axios
        .$get("summary/like/" + summary)
        .then((res) => {
          this.itemsTable = res;
        });
    },
    async deleteTask(id) {
      const response = await this.$axios.$delete("tasks/" + id);
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
