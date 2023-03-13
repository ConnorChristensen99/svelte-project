<script>

    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()
    export let todo
    let editing = false                     
    let name = todo.name                   
    function update(updatedTodo) {
      todo = { ...todo, ...updatedTodo }    
      dispatch('update', todo)             
    }
    function onCancel() {
      name = todo.name                     
      editing = false
    }
    function onSave() {
      update({ name: name })
      editing = false
    }
    function onRemove() {
      dispatch('remove', todo) 
    }
    function onEdit() {
      editing = true    
    }
    function onToggle() {
      update({ completed: !todo.completed}) 
    }

  </script>
  



  <div id="todos">
  {#if editing}

    <form on:submit|preventDefault={onSave}>
      <div>
        <label for="todo-{todo.id}" class="todo-label">New name for todo: </label>
        <input bind:value={name} type="text" id="todo-{todo.id}" class="newInput"/>
      </div>
      <div>
        <button on:click={onCancel} type="button"> Cancel </button>
        <button type="submit">
          Save
        </button>
      </div>
    </form>

  {:else}

    <div id="todoInfo">
      <label for="todo-{todo.id}" class="todo-label">{todo.id}. &nbsp;{todo.name}</label>
      <input type="checkbox" id="todo-{todo.id}" class="checkbox"
        on:click={onToggle} checked={todo.completed}
      >
    </div>
    <div id="endButtons">
      <button on:click={onEdit}>Edit</button>
      <button on:click={onRemove}>Delete</button>
    </div>
  {/if}
  </div>

  <style>
   .todo-label {
    font-size: x-large;
   }
   button {
    margin-left: 10px;
   }
   #endButtons {
    margin-right: -165px;
   }
   .checkbox {
        margin-left: 70px;
    }
    .newInput {
        margin-left: 25px;
        padding: 3%;
    }
    #todos {
        column-count: 2;
    }
    #todoInfo {
        display: flex;
        justify-content: space-between;
    }
  </style>