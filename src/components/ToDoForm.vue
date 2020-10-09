<template>
  <div class="main">
    <div class="container">
      <div class="todo-list">
        <h2>{{ msg }}</h2>
        <form @submit.prevent="addNewTodo" class="form">
          <div class="form-content">
            <input type="text" name="newTodo" placeholder="Add a new ToDo" aria-label="Add ToDo" v-model="newTodo" />
            <button class="btn btn-green">+ ADD</button>
          </div>
        </form>
        <div class="btn-group">
          <button class="btn btn-dark-green" @click="markAllDone">Mark All Done</button>
          <button class="btn btn-red" @click="removeAllTodos">Remove All ToDos</button>
        </div>
        <ul class="list-none">
          <li v-for="(todo, index) in todos" :key="todo.id" :class="todo">
            <h3 :class="{ todo, done: todo.done }" @click="toggleDone(todo)" title="Click to mark a task as done or to redo it">{{todo.content}}</h3>
            <button class="btn btn-outline-red" @click="removeTodo(index)">Delete</button>
          </li>
        </ul>
      </div>
    </div>
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

    function markAllDone () {
      todos.value.forEach((todo) => (todo.done = true))
    }

    function removeAllTodos () {
      todos.value = []
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos
    }
  },

  name: 'ToDoForm',
  props: {
    msg: String,
    warning: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h2 {
  color: rgb(34, 84, 61);
  font-weight: 400;
  padding: 1rem 0;
  text-align: center;
}

h3:hover {
  color: rgb(74, 85, 104);
}

.form {
  min-width: 24rem;
  width: 100%;

  & .form-content {
    align-items: center;
    border-bottom: 1px solid rgb(72, 187, 120);
    display: flex;
    padding: .5rem 0 .5rem;

    input {
      appearance: none;
      background: transparent;
      border: none;
      color: rgb(74, 85, 104);
      font-size: calc(1rem + 1vmin);
      line-height: 1.25rem;
      margin-right: .75rem;
      padding: .25rem .5rem;
      width: 100%;

      &:focus {
        outline: 0;
      }
    }
  }
}

/** button styles **/
.btn-group {
  display: flex;
  justify-content: center;
  margin: 1rem 0;
}

.btn {
  align-items: center;
  appearance: button;
  border: 0; // 1px solid transparent;
  border-radius: .25rem;
  color: rgb(0, 0, 0);
  display: inline-block;
  font-size: calc(1rem + 1vmin);
  font-weight: 700;
  justify-content: center;
  margin: .25rem 0;
  padding: .5rem 1rem;
  text-align: center;
  text-transform: none;
  transition: all .15s ease-in-out;
  user-select: none;
  vertical-align: middle;
  -webkit-appearance: button;
  -moz-appearance: button;
  -ms-appearance: button;
  -webkit-transition: all .15s ease-in-out;
  -moz-transition: all .15s ease-in-out;
  -ms-transition: all .15s ease-in-out;
  -webkit-tap-highlight-color: transparent;
  -moz-tap-highlight-color: transparent;
  -ms-tap-highlight-color: transparent;

  &:last-child {
    margin-left: .5rem;
  }

  &:focus {
    border-color: rgb(246, 135, 179) !important;
  }

  &:not(:disabled):not(.disabled), button:not(:disabled) {
    cursor: pointer;
  }

  &.btn-green {
    background-color: rgb(72, 187, 120);
    border-radius: .25rem;
    border-bottom: 4px !important;
    color: rgb(255, 255, 255);
    flex-shrink: 0;

    &:hover {
      background-color: rgb(47, 133, 90);
      border-color: rgb(47, 133, 90);
    }
  }

  &.btn-dark-green {
    background-color: rgb(34, 84, 61);
    border-radius: .25rem;
    border-bottom: 4px !important;
    color: rgb(255, 255, 255);
    flex-shrink: 0;

    &:hover {
      background-color: rgb(47, 133, 90);
      border-color: rgb(47, 133, 90);
    }
  }

  &.btn-red {
    background-color: rgb(245, 101, 101);
    border-radius: .25rem;
    border-bottom: 4px !important;
    color: rgb(255, 255, 255);
    flex-shrink: 0;

    &:hover {
      background-color: rgb(197, 48, 48);
      border-color: rgb(197, 48, 48);
    }
  }

  &.btn-outline-red {
    background-color: transparent;
    border: 1px solid rgb(245, 101, 101);
    border-radius: .25rem;
    color: rgb(245, 101, 101);
    flex-shrink: 0;

    &:hover {
      color: rgb(255, 255, 255);
      background-color: rgb(245, 101, 101);
      border-color: rgb(245, 101, 101);
    }
  }
}

.list-none {
  font-weight: 700;
  list-style: none;

  li {
    align-items: center;
    display: grid;
    grid-template-columns: repeat(3, 1fr);

    .done {
      color: rgb(74, 85, 104);
      text-decoration: line-through;
    }

    .todo {
      cursor: pointer;
      grid-column: 1 / span 2;
    }

    button {
      grid-column: 3 / span 3;
    }
  }
}
</style>
