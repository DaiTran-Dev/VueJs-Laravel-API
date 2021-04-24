<template>
  <div>
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
</template>

<script>
import ModalTitleCreateTask from "../../components/task/ModalTitleCreateTask";
import ListTaskTable from "../../components/task/ListTaskTable.vue";
import { BASE_API } from "../../constant/constant";

export default {
  data() {
    return {
      baseApi: BASE_API,
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
      console.log("asd");
      const response = await this.$axios.$get(this.baseApi);
      this.itemsTable = response;
    },
    async getTaskBySummary(summary) {
      var url = this.baseApi + "/summary/like/" + summary;
      const response = await this.$axios.$get(url).then((res) => {
        this.itemsTable = res;
      });
    },
    async deleteTask(id) {
      var url = this.baseApi + "/" + id;
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
