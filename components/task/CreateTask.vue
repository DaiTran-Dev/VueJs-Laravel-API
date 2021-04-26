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
            :options="constant.PROJECT"
            size="sm"
            :state="errorTask[0].status"
            aria-describedby="input-live-help input-live-feedback-project"
            placeholder="Enter your name"
            trim
          ></b-form-select>
          <b-form-invalid-feedback id="input-live-feedback-project">
            {{ errorTask[0].message }}
          </b-form-invalid-feedback>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Issue Type</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedIssue"
            :options="constant.ISSUE"
            size="sm"
            :state="errorTask[1].status"
            aria-describedby="input-live-help input-live-feedback-issue"
            placeholder="Enter your name"
            trim
          ></b-form-select>
          <b-form-invalid-feedback id="input-live-feedback-issue">
            {{ errorTask[1].message }}
          </b-form-invalid-feedback>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label>Summary:</label>
        </b-col>
        <b-col sm="8">
          <b-form-input
            type="text"
            size="sm"
            v-model="summary"
            :state="errorTask[3].status"
            aria-describedby="input-live-help input-live-feedback-summary"
            placeholder="Enter your name"
            trim
          ></b-form-input>
          <b-form-invalid-feedback id="input-live-feedback-summary">
            {{ errorTask[3].message }}
          </b-form-invalid-feedback>
        </b-col>
      </b-row>
      <b-row class="my-1">
        <b-col sm="2">
          <label for="input-none">Reporter</label>
        </b-col>
        <b-col sm="5">
          <b-form-select
            v-model="selectedReporter"
            :options="constant.REPORTER"
            size="sm"
            :state="errorTask[2].status"
            aria-describedby="input-live-help input-live-feedback-reporter"
            placeholder="Enter  reporter"
            trim
          ></b-form-select>
          <b-form-invalid-feedback id="input-live-feedback-reporter">
            {{ errorTask[2].message }}
          </b-form-invalid-feedback>
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
            :options="constant.ASSIGNEE"
            size="sm"
          ></b-form-select>
        </b-col>
      </b-row>
      <div class="footer-modal">
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
      </div>
    </b-form>
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
  ERROR_TASK,
} from "../../constant/constant.js";

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
      errorTask: ERROR_TASK,
      createAnother: false,
    };
  },
  props: ["activeForm", "taskId", "btnOpen"],
  computed: {
    constant() {
      return {
        ASSIGNEE: ASSIGNEE,
        BASE_API: BASE_API,
        FIELDS_TABLE_TASK: FIELDS_TABLE_TASK,
        REPORTER: REPORTER,
        ISSUE: ISSUE,
        PROJECT: PROJECT,
      };
    },
  },
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
    setDataForm(task = null) {
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
    resetForm() {
      this.summary = "";
      this.selectedProject = null;
      this.selectedIssue = null;
      this.selectedAssignee = null;
      this.selectedReporter = null;
      this.dueDate = "";
      this.desscription = "";
      this.attachment = "";
    },
    onSubmit(event) {
      event.preventDefault();
      var task = this.getDataForm();
      if (this.taskId == null) {
        this.createTask(task);
      } else {
        this.updateTask(this.taskId, task);
      }
    },
    onReset(event) {
      event.preventDefault();
      this.resetForm();
    },
    async createTask(task) {
      const response = await this.$axios
        .$post(this.constant.BASE_API, task)
        .then((res) => {
          var createAnother = (this.createAnother=='true');
          if (createAnother) {
            this.resetForm();
          } else {
            this.$bvModal.hide("modal-create-issue");
          }
          this.eventLoadTableTask();
          this.resethandlingError();
        })
        .catch(({ response: err }) => {
          console.log("fail");
          this.handlingError(err);
        });
    },
    async updateTask(taskId, task) {
      var url = this.constant.BASE_API + "/" + taskId;
      const response = await this.$axios
        .$put(url, task)
        .then((res) => {
          this.$bvModal.hide("modal-create-issue");
          this.eventLoadTableTask();
          this.resethandlingError();
        })
        .catch(({ response: err }) => {
          this.handlingError(err);
        });
    },
    async findTask(taskId) {
      if (taskId != null) {
        var url = this.constant.BASE_API + "/" + taskId;
        const response = await this.$axios.$get(url);
        this.setDataForm(response);
      }
    },
    eventLoadTableTask() {
      this.$emit("load-table", true);
    },
    formatFileNames(files) {
      return files.length === 1
        ? files[0].name
        : `${files.length} files selected`;
    },
    resethandlingError() {
      this.errorTask.forEach((error) => {
        error.status = null;
      });
    },
    handlingError(error) {
      var listErroResponse = new Array(error.data.errors)[0];
      //set error
      this.errorTask.forEach((error) => {
        if (listErroResponse.hasOwnProperty(error.name)) {
          error.status = false;
          error.message = listErroResponse[error.name][0];
        }
      });
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
  padding: 0 40px;
}
.footer-modal {
  border-top: 1px solid #dee2e6;
  padding: 20px;
  padding-bottom: 0;
  margin-top: 20px;
  justify-content: flex-end;
}
</style>
