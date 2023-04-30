<template>
  <div class="container col-lg-6 mt-3">
    <todo-heading></todo-heading>
    <form @submit.prevent="addTask">
      <div class="input-group mb-2">
        <input
          type="text"
          class="form-control"
          :placeholder="userCue"
          aria-label="Add Task"
          aria-describedby="basic-addon2"
          v-model.trim="userTask"
        />
        <button
          class="input-group-text btnBg text-white"
          id="basic-addon2"
          type="submit"
        >
          Add Task
        </button>
      </div>
      <Warning-Message>
        {{ checker ? `oops! you cannot add an empty task` : "" }}
      </Warning-Message>

      <div>
        <ul
          v-for="(taskItem, index) in addedTask"
          :key="taskItem.id"
          class="list-unstyled"
        >
          <li class="shadow bg-white p-3 d-flex justify-content-between">
            {{ taskItem.task }}
            <div>
              <delete-task @delete-task="del(index)"></delete-task>
              <edit-task @edit-task="edit(index)"></edit-task>
            </div>
          </li>
        </ul>
      </div>
    </form>
    <teleport to="body"
      ><dialogue-box
        id="#exampleModal"
        v-if="showModal"
        :task="taskToEdit"
        @update-task="updateTask"
        @close-modal="closeModal"
      ></dialogue-box
    ></teleport>
  </div>
</template>
<script>
let id = 0;
import DialogueBox from "./DialogueBox.vue";
import WarningMessage from "./WarningMessage.vue";
import TodoHeading from "./TodoHeading.vue";
import DeleteTask from "./DeleteTask.vue";
import EditTask from "./EditTask.vue";

export default {
  components: {
    WarningMessage,
    TodoHeading,
    DeleteTask,
    EditTask,
    DialogueBox,
  },

  data() {
    return {
      userTask: "",
      userCue: "what task would you like to add?",
      addedTask: [{ id: id++, task: "Learn Vuejs Today" }],
      checker: false,
      showModal: false,
      taskToEdit: "",
      taskToEditIndex: null,
    };
  },

  methods: {
    addTask() {
      if (this.userTask === "") {
        this.checker = true;
      } else {
        return (
          (this.checker = false),
          this.addedTask.unshift({ id: id++, task: this.userTask }),
          (this.userTask = "")
        );
      }
    },
    del(index) {
      this.addedTask.splice(index, 1);
    },
    edit(index) {
      console.log(index);
      this.taskToEdit = this.addedTask[index].task;
      this.taskToEditIndex = index;
      this.showModal = true;
    },
    updateTask(task) {
      if (this.taskToEdit === "") {
        return (this.editChecker = true);
      }
      this.addedTask.splice(this.taskToEditIndex, 1, {
        id: this.taskToEditIndex,
        task: task,
      });
    },
    closeModal() {
      this.showModal = false;
      this.taskToEdit = "";
      this.taskToEditIndex = null;
    },
  },
};
</script>

<style scoped>
.form-control {
  box-shadow: none !important;
  height: 45px;
}
.btnBg {
  background-color: #0077b6;
}
</style>
