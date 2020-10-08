<template>
  <div class="todo">
    <h1>{{ msg }}</h1>
    <form @submit.prevent="addNewTodo">
      <label for="newTodo">New ToDo</label>
      <input type="text" name="newTodo" />
      <button>Add new ToDo</button>
    </form>
  </div>
</template>

<script>
export default {
  setup () {
    function addNewTodo () {
      console.log('form was submitted')
    }

    return {
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
