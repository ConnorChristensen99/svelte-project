<script>
    import Todo from './Todo.svelte'
    export let todos = []
    
    let newTodoName = ''
    $: newTodoId = totalTodos ? Math.max(...todos.map(t => t.id)) + 1 : 1
    $: totalTodos = todos.length
    $: completedTodos = todos.filter(todo => todo.completed).length

    //Removes a todo
    function removeTodo(todo) {
      todos = todos.filter(t => t.id !== todo.id)
    }

    //Adds a todo
    function addTodo() {
      todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }]
      newTodoName = ''
    }

    //Clears all todos
    function removeCompleted() {
        todos = todos.filter(todo => !todo.completed == true)
    }

    //Updates a todo
    function updateTodo(todo) {
      const i = todos.findIndex(t => t.id === todo.id)
      todos[i] = { ...todos[i], ...todo }
    }
    let filter = 'all'
    const filterTodos = (filter, todos) => 
      filter === 'active' ? todos.filter(t => !t.completed) :
      filter === 'completed' ? todos.filter(t => t.completed) : 
      todos
  </script>
  


  <!-- Todos.svelte -->
  <div class="todoapp">
  
    <!-- NewTodo -->
    <form on:submit|preventDefault={addTodo}>
      <input bind:value={newTodoName} type="text" id="todo-0" placeholder="Please enter a todo..."/>
      <button class="add">
        Add
      </button>
    </form>
  

    
    <div id="labels">
    <span>Todo Name</span>
    <span>Completed</span>
    <span>Actions</span>
    </div>



    <!-- Todos -->
    <ul>
    {#each filterTodos(filter, todos) as todo (todo.id)}
      <li class="todo">
        <Todo {todo}
          on:update={e => updateTodo(e.detail)}
          on:remove={e => removeTodo(e.detail)}
        />
      </li>
    {/each}
    </ul>
  

    <!-- Header for todos to be completed -->
    <h2 id="list-heading">{completedTodos} out of {totalTodos} items completed</h2>


    <!-- Button to remove todos -->
    <div class="btn-group">
      <button type="button" on:click={() => removeCompleted()}>Remove completed</button>
    </div>
  
  </div>

  


  <!-- Styling -->
  <style>

    ul {
        list-style-type: none;
        display: flex;
        flex-wrap: wrap;
    }

    ul li {
        margin: 30px 0 10px 0;
        margin-right: 5%;
        border: 1px solid rgb(214, 214, 214);
        padding: 3%;
        width: 100%;
    }
   .add {
    margin-left: 15px;
   }
   #todo-0 {
    padding: 2%;
   }
   #labels {
    padding-top: 10%;
    margin-bottom: -40px;
    display: flex;
    justify-content: space-around;
    max-width: 800px;
   }
   .addTodoss {
    margin-top: 3%;
   }
  </style>