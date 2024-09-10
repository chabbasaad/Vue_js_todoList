<template>
  <div>
  <h1>To-Do List</h1>

    <form @submit.prevent="addTask">
      <input
        v-model="newTask"
        type="text"
        placeholder="Enter a new task"
        required
      />
      <button type="submit">Add Task</button>
    </form>

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
        <button @click="deleteTask(task.id)">Delete</button>
        <button @click="toggleComplete(task)">{{ task.completed ? 'Undo' : 'Complete' }}</button>
      </li>
    </ul>
  </div>

</template>

<!-- method support vue js 2 and 3 -->
<!-- <script >
import axios from "axios";

export default {
  data() {
    return {
      tasks: [],
      newTask: "",
    };
  },
  mounted() {
    this.getTasks();
  },
  methods: {
    // Fetch all tasks from JSON Server
    async getTasks() {
      const response = await axios.get("http://localhost:3000/tasks");
      this.tasks = response.data;
    },

    // Add a new task
    async addTask() {
      const newTaskObj = {
        title: this.newTask,
        completed: false,
      };
      const response = await axios.post("http://localhost:3000/tasks", newTaskObj);
      this.tasks.push(response.data);
      this.newTask = "";
    },

    // Delete a task
    async deleteTask(id) {
      await axios.delete(`http://localhost:3000/tasks/${id}`);
      this.tasks = this.tasks.filter(task => task.id !== id);
    },

    // Toggle task completion
    async toggleComplete(task) {
      task.completed = !task.completed;
      await axios.put(`http://localhost:3000/tasks/${task.id}`, task);
    }
  },
};
</script> -->

<!-- <script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const tasks = ref([]);
    const newTask = ref("");

    // Fetch tasks when the component is mounted
    const getTasks = async () => {
      const response = await axios.get("http://localhost:3000/tasks");
      tasks.value = response.data;
    };

    // Add a new task
    const addTask = async () => {
      const newTaskObj = {
        title: newTask.value,
        completed: false,
      };
      const response = await axios.post("http://localhost:3000/tasks", newTaskObj);
      tasks.value.push(response.data);
      newTask.value = ""; // Clear input after adding
    };

    // Delete a task
    const deleteTask = async (id) => {
      await axios.delete(`http://localhost:3000/tasks/${id}`);
      tasks.value = tasks.value.filter((task) => task.id !== id);
    };

    // Toggle task completion
    const toggleComplete = async (task) => {
      task.completed = !task.completed;
      await axios.put(`http://localhost:3000/tasks/${task.id}`, task);
    };

    onMounted(() => {
      getTasks();
    });

    return {
      tasks,
      newTask,
      addTask,
      deleteTask,
      toggleComplete,
    };
  },
};
</script> -->

<!-- 3 option for using axio -->
<script setup>

import { ref, onMounted } from "vue";
import axios from "axios";


const tasks = ref([]);

onMounted(() => {

  getTasks();

});

// Fetch tasks when the component is mounted
const getTasks = async () => {
      const response = await axios.get("http://localhost:3000/tasks");
      tasks.value = response.data;
    };

  
       // Add a new task
       const addTask = async () => {
      const newTaskObj = {
        title: newTask.value,
        completed: false,
      };
      const response = await axios.post("http://localhost:3000/tasks", newTaskObj);
      tasks.value.push(response.data);
      newTask.value = ""; // Clear input after adding
    };

    // Delete a task
    const deleteTask = async (id) => {
      await axios.delete(`http://localhost:3000/tasks/${id}`);
      tasks.value = tasks.value.filter((task) => task.id !== id);
    };

    // Toggle task completion
    const toggleComplete = async (task) => {
      task.completed = !task.completed;
      await axios.put(`http://localhost:3000/tasks/${task.id}`, task);
    };



</script>



<style scoped>
.completed {
  text-decoration: line-through;
}
</style>