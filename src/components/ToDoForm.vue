<template>
  <div class="todo">
    <h1>{{ msg }}</h1>
    <form @submit.prevent="addNewTodo">
      <label for="newTodo">New ToDo</label>
      <input type="text" name="newTodo" v-model="newTodo" />
      <button>Add new ToDo</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const newTodo = ref('')
    const todos = ref([])

    function addNewTodo () {
      todos.value.push({
        done: false,
        content: newTodo.value
      })
    }

    return {
      todos,
      newTodo,
      addNewTodo
    }
  },

  name: 'ToDoForm',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
