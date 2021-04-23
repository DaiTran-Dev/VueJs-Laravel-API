<template>
  <div>
    <ModalTitleCreateTask title="Task" :taskId="taskId" @click-create="editAction($event)"></ModalTitleCreateTask>
    <ListTaskTable class="mt-5" :itemsTable="itemsTable" @click-edit="editAction($event)"></ListTaskTable>
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
      itemsTable:[],
      taskId:null,
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
    editAction(id){
      this.taskId = id;
      this.$bvModal.show("modal-create-issue");
    },
  },
  mounted(){
    this.getAllTask();
  }
};
</script>
<style>
</style>
