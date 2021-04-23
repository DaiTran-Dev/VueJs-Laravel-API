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
      <template #cell(project)="project_id">
        {{ getNameById(project_id.value, constantSystem.PROJECT) }}
      </template>
      <template #cell(issue_type)="issue_type_id">
        {{ getNameById(issue_type_id.value, constantSystem.ISSUE) }}
      </template>
      <template #cell(reporter)="reporter_id">
        {{ getNameById(reporter_id.value, constantSystem.REPORTER) }}
      </template>
      <template #cell(assignee)="assignee_id">
        {{ getNameById(assignee_id.value, constantSystem.ASSIGNEE) }}
      </template>
      <template #cell(edit)="row">
        <b-button
          variant="outline-success"
          type="button"
          @click="$emit('click-edit', row.item.id)"
          >Edit</b-button
        >
      </template>
      <template #cell(delete)="row">
        <b-button
          variant="outline-danger"
          type="button"
          @click="$emit('click-delete', row.item.id)"
          >Delete</b-button
        >
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
  methods: {
    getNameById($id, $array = []) {
      var result = $array.find(($x) => {
        return $x.value == $id;
      });
      if (result) {
        return result.text;
      }
    },
  },
};
</script>

