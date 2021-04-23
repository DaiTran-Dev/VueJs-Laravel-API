<template>
  <div>
    <b-table
      :items="itemsTable"
      :fields="constantSystem.FIELDS_TABLE_TASK"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      responsive="sm"
      bordered
    >
       <template #cell(edit)="row">
          <b-button variant="outline-success" type="button" @click="$emit('click-edit',row.item.id)">Edit</b-button>
      </template>
      <template #cell(delete)>
        <b-button variant="outline-danger" type="button">Danger</b-button>
      </template>
    </b-table>
  </div>
</template>
<script>
import constantSystem from "../../constant/constantSystem.vue";
export default {
  data() {
    return {
      sortBy: "age",
      sortDesc: false,
      constantSystem: constantSystem,
    };
  },
  props: ["itemsTable"],
};
</script>

