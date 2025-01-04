<template>
  <div id="app" class="container">
    <h1>Vue.js To-Do List</h1>
    <div class="input-container">
      <input v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask" />
      <button @click="addTask" class="btn btn-add"><i class="fas fa-plus"></i></button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
        <input type="checkbox" v-model="task.completed" id="checkbox" />

        <span v-if="!task.isEditing" class="task-text">{{ task.text }}</span>
        <input v-else v-model="task.text" @keyup.enter="saveTask(task)" @blur="saveTask(task)" class="edit-input" />

        <div class="actions">
          <button v-if="!task.isEditing" @click="editTask(task)" class="btn btn-edit"><i class="fas fa-edit"></i></button>
          <button @click="removeTask(index)" class="btn btn-delete"><i class="fas fa-trash-alt"></i></button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false, isEditing: false });
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(task) {
      task.isEditing = true;
    },
    saveTask(task) {
      task.isEditing = false;
    }
  }
};
</script>

<style>
body {
  background-color: #f4f7f6;
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  padding: 20px;
  max-width: 400px;
  width: 100%;
}

h1 {
  color: #333;
  margin-bottom: 20px;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

.btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 5px;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #45a049;
}

.btn-add {
  background-color: #28a745;
}

.btn-edit {
  background-color: #ffc107;
}

.btn-delete {
  background-color: #dc3545;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 5px;
  background-color: #f8f9fa;
}

li.completed .task-text {
  text-decoration: line-through;
  color: #888;
}

li:hover {
  background-color: #e9ecef;
}

.actions {
  display: flex;
}

.actions .btn {
  margin-left: 5px;
}

.edit-input {
  flex: 1;
  margin-right: 10px;
}
</style>