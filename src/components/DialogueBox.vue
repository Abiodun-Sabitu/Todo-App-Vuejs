<template>
  <div class="modal" tabindex="-1">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Edit Task</h5>
        </div>
        <div class="modal-body">
          <textarea v-model="updatedTask" class="form-control"></textarea>
          <warning-message class="mt-2">
            <template v-slot:warning>
              {{ editChecker ? `Oops! the editable area cannot be empty` : "" }}
            </template>
          </warning-message>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-danger"
            data-bs-dismiss="modal"
            @click="closeModal"
          >
            Close
          </button>
          <button type="button" class="btn btnBg" @click="updateTask">
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import WarningMessage from "./WarningMessage.vue";
export default {
  components: {
    WarningMessage,
  },
  emits: ["update-task", "close-modal"],
  props: {
    task: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      updatedTask: this.task,
      editChecker: false,
    };
  },
  methods: {
    updateTask() {
      console.log(this.updatedTask.length);
      if (this.updatedTask.length === 0) {
        this.editChecker = true;
      } else {
        this.$emit("update-task", this.updatedTask);
        this.closeModal();
      }
    },
    closeModal() {
      this.$emit("close-modal");
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1060;
  display: block;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  outline: 0;
}

.btnBg {
  background-color: #0077b6;
  color: white;
}
</style>
