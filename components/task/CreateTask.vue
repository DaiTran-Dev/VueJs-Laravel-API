<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" id="form-create">
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Project:</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedProject"
            :options="options"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Issue Type</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedIssue"
            :options="option"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="2">
          <label>Summary:</label>
        </b-col>
        <b-col sm="8">
          <b-form-input type="text" size="sm"></b-form-input>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Reporter</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedReporter"
            :options="option"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">attchment</label>
        </b-col>
        <b-col sm="8">
          <b-form-file :file-name-formatter="formatFileNames"></b-form-file>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Due Date</label>
        </b-col>
        <b-col sm="4">
          <b-form-datepicker
            id="example-datepicker"
            v-model="dueDate"
            class="mb-2"
          ></b-form-datepicker>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Desscription</label>
        </b-col>
        <b-col sm="8">
          <b-form-textarea
            id="textarea"
            v-model="desscription"
            placeholder="Enter something..."
            rows="5"
            max-rows="7"
            class="form-control"
          ></b-form-textarea>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Assignee</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedAssignee"
            :options="option"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedProject: null,
      selectedIssue: null,
      selectedReporter: null,
      selectedAssignee: null,
      desscription:'',
      dueDate: "",
      options: [
        { value: null, text: "Please select an option" },
        { value: "a", text: "This is First option" },
        { value: "b", text: "Selected Option" },
        { value: { C: "3PO" }, text: "This is an option with object value" },
        { value: "d", text: "This one is disabled", disabled: true },
      ],
      option: [
        { value: null, text: "Please select an option" },
        { value: "a", text: "This is First option" },
        { value: "b", text: "Selected Option" },
        { value: { C: "3PO" }, text: "This is an option with object value" },
        { value: "d", text: "This one is disabled", disabled: true },
      ],
    };
  },
  props: ["activeCreate"],
  methods: {
    onSubmit(event) {
      if (activeCreate) {
        console.log("ok insert");
      } else {
        console.log("no insert");
      }
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.food = null;
      this.form.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    formatFileNames(files) {
      return files.length === 1
        ? files[0].name
        : `${files.length} files selected`;
    },
  },
};
</script>
<style>
#form-create .my-1 {
  margin-bottom: 20px !important;
}
</style>
