<template>
  <div>
    <b-table
      :items="itemsTable"
      :fields="constant.FIELDS_TABLE_TASK"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      responsive="sm"
      bordered
    >
      <template #cell(project)="project_id">
        {{ getNameById(project_id.value, constant.PROJECT) }}
      </template>
      <template #cell(issue_type)="issue_type_id">
        {{ getNameById(issue_type_id.value, constant.ISSUE) }}
      </template>
      <template #cell(reporter)="reporter_id">
        {{ getNameById(reporter_id.value, constant.REPORTER) }}
      </template>
      <template #cell(assignee)="assignee_id">
        {{ getNameById(assignee_id.value, constant.ASSIGNEE) }}
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
import {
  ASSIGNEE,
  BASE_API,
  FIELDS_TABLE_TASK,
  REPORTER,
  ISSUE,
  PROJECT,
} from "../../constant/constant.js";

export default {
  data() {
    return {
      sortBy: "age",
      sortDesc: false,
      constant: {
        ASSIGNEE: ASSIGNEE,
        BASE_API: BASE_API,
        FIELDS_TABLE_TASK: FIELDS_TABLE_TASK,
        REPORTER: REPORTER,
        ISSUE: ISSUE,
        PROJECT: PROJECT,
      },
    };
  },
  props: ["itemsTable"],
  methods: {
    getNameById(id, $listMaster = []) {
      var result = $listMaster.find((item) => {
        return item.value == id;
      });
      if (result) {
        return result.text;
      }
    },
  },
};
</script>

