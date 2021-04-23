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
            :options="constantSystem.PROJECT"
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
            :options="constantSystem.ISSUE"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="2">
          <label>Summary:</label>
        </b-col>
        <b-col sm="8">
          <b-form-input type="text" size="sm" v-model="summary"></b-form-input>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Reporter</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedReporter"
            :options="constantSystem.REPORTER"
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
            :options="constantSystem.ASSIGNEE"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>
      <b-row class="footer-modal">
        <div class="d-flex justify-content-end">
          <b-form-checkbox
            v-model="createAnother"
            name="createAnother"
            value="true"
            unchecked-value="false"
            class="mr-4"
          >
            <span class="text-nowrap">Create Another</span>
          </b-form-checkbox>
          <b-button type="submit" variant="primary" class="mr-3" size="sm"
            >Create</b-button
          >
          <b-button type="reset" variant="danger">Cancel</b-button>
        </div>
      </b-row>
    </b-form>
  </div>
</template>

<script>
import constantSystem from "../../constant/constantSystem.vue";
export default {
  data() {
    return {
      selectedProject: null,
      selectedIssue: null,
      selectedReporter: null,
      selectedAssignee: null,
      desscription: "",
      dueDate: "",
      summary: "",
      constantSystem: constantSystem,
      createAnother: false,
    };
  },
  props: ["activeForm", "taskId", "btnOpen"],
  methods: {
    getDataForm() {
      var task = {
        project_id: this.selectedProject,
        issue_type: this.selectedIssue,
        assignee: this.selectedAssignee,
        reporter: this.selectedReporter,
        due_date: this.dueDate,
        description: this.desscription,
        attachment: "https://picsum.photos/200/300",
        summary: this.summary,
      };
      return task;
    },
    setDataForm(task) {
      if (task) {
        this.summary = task.summary;
        this.selectedProject = task.project;
        this.selectedIssue = task.issue_type;
        this.selectedAssignee = task.assignee;
        this.selectedReporter = task.reporter;
        this.dueDate = task.due_date;
        this.desscription = task.description;
        this.attachment = task.attachment;
      }
    },
    onSubmit(event) {
      event.preventDefault();
      var task = this.getDataForm();
      if (this.taskId == null) {
        this.createTask(task);
      } else {
        this.updateTask(this.taskId,task);
      }
    },
    onReset(event) {
      event.preventDefault();
    },
    async createTask(task) {
      const response = await this.$axios
        .$post(this.constantSystem.BASE_API, task)
        .then((res) => {
          console.log("success");
          console.log(res);
        })
        .catch(({ response: err }) => {
          console.log("fail");
          console.log(err);
        });
    },
    async updateTask(taskId,task) {
      console.log(task);
      var url = this.constantSystem.BASE_API + "/" + taskId;
      const response = await this.$axios
        .$put(url, task)
        .then((res) => {
          console.log("success");
          console.log(res);
        })
        .catch(({ response: err }) => {
          console.log("fail");
          console.log(err);
        });
    },
    async findTask(taskId) {
      if (taskId != null) {
        var url = this.constantSystem.BASE_API + "/" + taskId;
        const response = await this.$axios.$get(url);
        this.setDataForm(response);
      }
    },
    formatFileNames(files) {
      return files.length === 1
        ? files[0].name
        : `${files.length} files selected`;
    },
  },
  mounted() {
    this.findTask(this.taskId);
  },
};
</script>
<style>
#form-create .my-1 {
  margin-bottom: 20px !important;
}
.footer-modal {
  border-top: 1px solid #dee2e6;
  padding-top: 20px;
  margin-top: 20px;
  justify-content: flex-end;
}
</style>
