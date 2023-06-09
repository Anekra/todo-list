<template>
  <div class="content">
    <div class="row">
      <h1 class="title">Todo List</h1>
    </div>
    <div class="row">
      <div v-if="isTasksEmptyAndIsNotCreating" class="empty-tasks">
        <h3>Belum ada task</h3>
      </div>
      <div v-else-if="isCreating" class="input-wrapper">
        <input
          v-model="titleValue"
          type="text"
          placeholder="title"
          class="input"
        />
        <textarea
          v-model="descriptionValue"
          placeholder="description"
          class="input"
        />
      </div>
      <div v-else v-for="(task, index) of tasks" class="task-list">
        <div class="divider">
          <hr />
        </div>
        <div class="task-item-wrapper">
          <div class="task-item">
            <input
              @click="toggleIsDone(index)"
              type="checkbox"
              :checked="task.isDone"
            />
          </div>
          <div class="task-item">
            <div class="task-item-title">
              <h3 class="task-title">
                <s v-if="task.isDone">{{ task.title }}</s>
                <span v-else>{{ task.title }}</span>
              </h3>
              <p>{{ task.description }}</p>
            </div>
            <div class="time">
              <h3>{{ getTime(task.createdAt) }}</h3>
            </div>
          </div>
          <div class="task-item">
            <button
              @click="deleteTask(index)"
              href="#"
              class="button btn-delete"
            >
              {{ task.delete }}
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div v-if="isCreating">
        <button @click="addTask" class="button btn-save">Save</button>
        <button @click="hideAddTask" class="button btn-cancel">Cancel</button>
      </div>
      <button v-else @click="showAddTask" class="button">Add task</button>
    </div>
  </div>
</template>

<script>
export default (await import('vue')).defineComponent({
  data() {
    return {
      tasks: [],
      isCreating: false,
      titleValue: '',
      descriptionValue: ''
    };
  },
  computed: {
    isTasksEmptyAndIsNotCreating() {
      return this.tasks.length === 0 && !this.isCreating;
    }
  },
  methods: {
    showAddTask() {
      this.isCreating = true;
    },
    hideAddTask() {
      this.isCreating = false;
    },
    addTask() {
      this.tasks.push({
        title: this.titleValue,
        description: this.descriptionValue,
        delete: 'Delete',
        isDone: false,
        createdAt: new Date()
      });
      this.titleValue = '';
      this.descriptionValue = '';
      this.isCreating = false;
    },
    deleteTask(index) {
      console.log(this.tasks[index]);
      this.tasks.splice(index, 1);
    },
    toggleIsDone(index) {
      this.tasks[index].isDone = !this.tasks[index].isDone;
    },
    getTime(time) {
      const month = time.toLocaleString('default', { month: 'short'});
      const date = time.getDate();
      const hour = time.getHours();
      const minute = time.getMinutes();

      return `${month} ${date}, ${hour}:${minute}`
    }
  }
});
</script>

<style>
s {
  text-decoration-color: rgb(0, 63, 26);
}
hr {
  width: 100%;
  margin-bottom: 10px;
}
.content {
  color: #cce8e7;
  font-size: 1rem;
  font-weight: 10;
  height: 100%;
  background-color: #324b4b;
  padding: 16px 16px;
  display: flex;
  flex: 1;
  flex-direction: column;
}
.row {
  flex: 1;
  width: 100%;
}
.row:first-child,
.row:last-child {
  flex: 1;
}
.row:last-child {
  display: flex;
  justify-content: space-around;
}
.row:nth-child(2) {
  display: flex;
  flex-direction: column;
  overflow: auto;
  flex: 0 0 80%;
}
.title {
  text-align: left;
  font-size: 2rem;
  align-self: flex-start;
}
.empty-tasks {
  width: calc(100% - 20px);
  height: calc(100% - 20px);
  display: flex;
  justify-content: center;
  align-items: center;
}
.input-wrapper {
  width: calc(100% - 20px);
  height: calc(100% - 20px);
  display: flex;
  flex-direction: column;
}
.input {
  width: 100%;
  max-width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}
.task-list {
  width: calc(100% - 20px);
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}
.task-list:first-child div.divider hr {
  display: none;
}
.task-item-wrapper {
  display: flex;
  justify-content: space-between;
}
.task-item:first-child {
  flex: 1;
  display: flex;
  justify-content: center;
}
.task-item:nth-child(2) {
  flex: 8;
  display: flex;
  justify-content: space-between;
}
.task-item-title {
  display: flex;
  flex-direction: column;
}
.time {
  margin-right: 20px;
  display: flex;
  align-items: center;
}
.button {
  appearance: button;
  background-color: #006468;
  border: solid transparent;
  border-radius: 16px;
  border-width: 0 0 4px;
  box-sizing: border-box;
  color: #c4fffc;
  cursor: pointer;
  display: inline-block;
  font-weight: bold;
  letter-spacing: 0.8px;
  margin-right: 10px;
  outline: none;
  padding: 13px 16px;
  text-align: center;
  text-transform: uppercase;
  touch-action: manipulation;
  transform: translateZ(0);
  user-select: none;
  -webkit-user-select: none;
  vertical-align: middle;
}
.btn-save {
  background-color: #003f31;
  color: #c6fbff;
}
.btn-cancel {
  background-color: #4d4d4d;
  color: #f5f5f5;
}
.btn-delete {
  background-color: #5a0000;
  color: #ffc7c7;
}
.button::after {
  background-clip: padding-box;
  background-color: #2cdfdf;
  border-radius: 16px;
  border-width: 0 0 4px;
  bottom: -4px;
  content: '';
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  z-index: -1;
}
.btn-save::after {
  background-color: #128b71;
}
.btn-cancel::after {
  background-color: #bdbdbd;
}
.btn-delete::after {
  background-color: #c53232;
}
.button:main,
.button:focus {
  user-select: auto;
}
.button:hover {
  filter: brightness(1.5);
  -webkit-filter: brightness(1.5);
  color: #003b3f;
}
.btn-save:hover {
  color: #004234;
}
.btn-cancel:hover {
  color: #5f5f5f;
}
.btn-delete:hover {
  color: #520000;
}
.button:disabled {
  cursor: auto;
}
</style>
