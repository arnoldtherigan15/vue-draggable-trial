<template>
    <div class="card-task uk-card uk-card-default uk-width-1-2@m">
        <div class="uk-card-header" :style="{ 'border-bottom': borderColor }">
            <div class="card-header">
                <div>
                    <img class="uk-border-circle" width="40" height="40" :src="`https://avatars.dicebear.com/api/avataaars/${task.author}.svg?style=circle`">
                </div>
                <div>
                    <h3 class="uk-card-title uk-margin-remove-bottom">{{ task.title }}</h3>
                    <p class="uk-text-meta uk-margin-remove-top"><time datetime="2016-04-01T19:00">{{ task.date }}</time></p>
                </div>
            </div>
        </div>
        <div class="uk-card-body" style="position:relative;">
            <p>{{ task.description }}</p>
            <h5 style="position:absolute; bottom:10px; right:10px">{{ task.author }} [{{ task.id }}]</h5>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: ['task'],
  computed: {
    borderColor () {
      let result = ''
      switch (this.task.category) {
        case 'backlog':
          result = '1px solid #f0506e'
          break
        case 'todo':
          result = '1px solid #faa05a'
          break
        case 'doing':
          result = '1px solid #1e87f0'
          break
        case 'done':
          result = '1px solid #32d296'
          break
      }
      return result
    }
  }
}
</script>

<style>

</style>
