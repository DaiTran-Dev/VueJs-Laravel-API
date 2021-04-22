<template>
  <div>
    <ModalTitleCreateTask title="Task"></ModalTitleCreateTask>
    <ListTaskTable class="mt-5"></ListTaskTable>
  </div>
</template>
<script>
import ModalTitleCreateTask from "../../components/task/ModalTitleCreateTask";
import ListTaskTable from "../../components/task/ListTaskTable.vue";

export default {
  components: {
    ModalTitleCreateTask,
    ListTaskTable,
  },
};
</script>
<style>
</style>
