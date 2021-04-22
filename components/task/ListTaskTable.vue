<template>
  <div>
    <b-table
      :items="items"
      :fields="fields"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      responsive="sm"
      bordered
    ></b-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      sortBy: "age",
      sortDesc: false,
      fields: [
        { key: "id", sortable: true },
        { key: "issue_type", sortable: true },
        { key: "summary", sortable: true },
        { key: "reporter", sortable: false },
        { key: "dueDate", sortable: true },
        { key: "assignee", sortable: true },
      ],
      items: [
        {
          isActive: true,
          age: 40,
          first_name: "Dickerson",
          last_name: "Macdonald",
        },
        { isActive: false, age: 21, first_name: "Larsen", last_name: "Shaw" },
        { isActive: false, age: 89, first_name: "Geneva", last_name: "Wilson" },
        { isActive: true, age: 38, first_name: "Jami", last_name: "Carney" },
      ],
    };
  },
};
</script>

