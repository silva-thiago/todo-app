<template>
  <div class="head todo">
    <img alt="Vue logo" src="../assets/logo.png">
    <ToDoForm msg="Welcome to Your Vue3 ToDo App" />
  </div>
</template>

<script>
// @ is an alias to /src
import ToDoForm from '@/components/ToDoForm.vue'

export default {
  name: 'ToDo',
  components: {
    ToDoForm
  }
}
</script>

<style lang="scss">
.head {
  display: grid;
  place-items: center;

  img {
    height: 4rem;
  }
}
</style>
