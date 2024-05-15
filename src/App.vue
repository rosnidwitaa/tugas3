<template>
  <div id="app">
    <div class="add-task">
      <input type="text" v-model="taskName" placeholder="Add New Task">
      <button @click="addTask">Add</button>
    </div>
    <div class="task-list">
      <div class="task-box">
        <ul>
          <li v-for="task in tasks" :key="task.id">
            <span>{{ task.name }}</span>
            <button @click="editTask(task)">Edit</button>
            <button @click="deleteTask(task.id)">Delete</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      taskName: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.taskName.trim()) {
        this.tasks.push({ id: Date.now(), name: this.taskName });
        this.taskName = '';
      }
    },
    editTask(updatedTask) {
      const newName = prompt('Enter new task name:', updatedTask.name);
      if (newName && newName.trim()) {
        updatedTask.name = newName.trim();
      }
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    }
  }
};
</script>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.add-task {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.add-task input[type="text"] {
  flex: 1;
  padding: 8px;
  margin-right: 10px;
}

.add-task button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-task button:hover {
  background-color: #45a049;
}

.task-list {
  display: flex;
  justify-content: center;
}

.task-box {
  border: 2px solid #ccc;
  padding: 20px;
  border-radius: 8px;
}

.task-list ul {
  list-style-type: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.task-list span {
  flex: 1;
}

.task-list button {
  padding: 4px 8px;
  background-color: #f44336;
  color: white;
  border: none;
  cursor: pointer;
  margin-left: 5px;
  transition: background-color 0.3s;
}

.task-list button:hover {
  background-color: #d32f2f;
}
</style>
