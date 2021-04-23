<script>
//Project
const PROJECT = [
  { value: "", text: "Please select an option" },
  { value: 1, text: "Demo project laravel" },
  { value: 2, text: "Project python" },
  { value: 3, text: "Project C#" },
];

//Issue Type
const ISSUE = [
  { value: "", text: "Please select an option" },
  { value: 1, text: "Task" },
  { value: 2, text: "Erros" },
  { value: 3, text: "Delay" },
];

// Reporter
const REPORTER = [
  { value: "", text: "Please select an option" },
  { value: 1, text: "Jonie [Admin]" },
  { value: 2, text: "Rel [Employee]" },
];

// Assignee
const ASSIGNEE = [
  { value: "", text: "Please select an option" },
  { value: 1, text: "Automatic" },
  { value: 2, text: "Rel Dai" },
];

//Fields table task
const FIELDS_TABLE_TASK = [
  { key: "id", sortable: true },
  { key: "project", sortable: true },
  { key: "issue_type", sortable: true },
  { key: "summary", sortable: true },
  { key: "reporter", sortable: true },
  { key: "due_date", sortable: true },
  { key: "assignee", sortable: true },
  { key: "edit", sortable: false },
  { key: "delete", sortable: false },
];

//Base url API
const BASE_API = "http://127.0.0.1:8000/api/tasks";
export default {
  BASE_API: BASE_API,
  PROJECT: PROJECT,
  REPORTER: REPORTER,
  ASSIGNEE: ASSIGNEE,
  ISSUE: ISSUE,
  FIELDS_TABLE_TASK: FIELDS_TABLE_TASK,
};
</script>
