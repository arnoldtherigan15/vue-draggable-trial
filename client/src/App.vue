<template>
    <div id="app">
        <div class="container">
            <Category v-for="(category, i) in categories" :key="i" :category="category" :tasks="tasks" @fetchTasks="fetchTasks" />
        </div>
    </div>
</template>

<script>
import Category from './components/Category.vue'
import axios from 'axios'
export default {
  data () {
    return {
      tasks: [],
      categories: ['backlog', 'todo', 'doing', 'done']
    }
  },
  components: {
    Category
  },
  methods: {
    fetchTasks () {
      axios({ method: 'get', url: 'http://localhost:3000/tasks' })
        .then(({ data }) => {
          this.tasks = data
        })
        .catch(err => {
          console.log(err, '>>>>>>>>>>>>> error')
        })
    }
  },
  created () {
    this.fetchTasks()
  }
}
</script>

<style>
    .container {
        display: flex;
        width: 100%;
        flex-wrap: wrap;
        justify-content: center;
    }
    .category {
        width: 20%;
        padding: 20px;
        margin: 30px 10px;
        height: 100%;
    }
    .card-task {
        margin: 20px auto;
        width: 100%;
        cursor: pointer;
    }
    .card-header {
        display: flex;
    }
</style>
