<script>
  import Todos from './lib/TodoList.svelte'
  let todos = [
    { id: 1, name: 'Walk the Dog', completed: true },
    { id: 2, name: 'Do the dishes', completed: true },
    { id: 3, name: 'Todo Svelte App', completed: false }
  ]
</script>

<h1>Todo App</h1>
<br>
<br>
<br>
<Todos {todos} />



<style>
</style>