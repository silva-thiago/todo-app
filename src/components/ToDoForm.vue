<template>
  <div class="todo">
    <h1>{{ msg }}</h1>
    <form @submit.prevent="addNewTodo">
      <label for="newTodo">New ToDo</label>
      <input type="text" name="newTodo" v-model="newTodo" />
      <button>Add new ToDo</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" :class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)" title="Click to mark a task as done or to redo it">{{todo.content}}</h3>
        <button @click="removeTodo(index)">Remove ToDo</button>
      </li>
    </ul>
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
        id: Date.now(), // it has a unique value, this is for test
        done: false,
        content: newTodo.value
      })
      newTodo.value = ''
    }

    function toggleDone (todo) {
      todo.done = !todo.done
    }

    function removeTodo (index) {
      todos.value.splice(index, 1)
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo
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
.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
