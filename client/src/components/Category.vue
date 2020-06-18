<template>
    <div class="category">
        <h1 class="uk-heading-line uk-text-center">
            <span class="uk-label" :style="{'background-color': color }">{{ category }}</span>
        </h1>
        <draggable :list="filterTask" group="task" :move="onMove" :category="category" @end="updateCategory">
            <Card v-for="task in filterTask" :key="task.id" :task="task" :id="task.id"/>
        </draggable>
    </div>
</template>

<script>
import Card from './Card'
import axios from 'axios'
import draggable from 'vuedraggable'
export default {
  name: 'Category',
  data() {
      return {
          currentId: null,
          currentCategory: null
      }
  },
  components: {
    Card,
    draggable
  },
  props: [
    'category', 'tasks'
  ],
  methods: {
      updateCategory() {
          axios({
              method: 'patch',
              url: `http://localhost:3000/tasks/${this.currentId}`,
              data: {
                  category: this.currentCategory
              }
          })
            .then(_=> {
                this.$emit('fetchTasks')
            })
            .catch(err => {
                console.log(err,'>>>>>>>>>>>>>> error');
                
            })
      },
      onMove(evt) {
          this.currentId = evt.draggedContext.element.id
          this.currentCategory = evt.relatedContext.component.$attrs.category
          
      }
  },
  computed: {
    color () {
      let result = ''
      switch (this.category) {
        case 'backlog':
          result = '#f0506e'
          break
        case 'todo':
          result = '#faa05a'
          break
        case 'doing':
          result = '#1e87f0'
          break
        case 'done':
          result = '#32d296'
          break
      }
      return result
    },
    filterTask () {
      const result = []
      this
        .tasks
        .forEach(task => {
          if (task.category === this.category) { result.push(task) }
        })
      return result
    }
  }
}
</script>

<style></style>
