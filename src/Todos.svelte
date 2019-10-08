<script>
  import TodoItem from "./TodoItem.svelte";

  let todos = [
    {
      id: 1,
      title: "Create a symphony",
      completed: false
    },
    {
      id: 2,
      title: "Make a svelte presentation",
      completed: true
    },
    {
      id: 3,
      title: "Be happy",
      completed: false
    }
  ];

  let newTodoTitle = "";
  let currentFilter = "all";
  let nextId = todos.length + 1;

  /**
   * @desc : function for adding task
   * @param: {event} e - the event when keydown enter is down
   **/
  const addTodo = e => {
    if (e.key === "Enter") {
      todos = [...todos, { id: nextId, title: newTodoTitle, completed: false }];
      newTodoTitle = "";
    }
  };


  const updateFilter = newFilter => {
   currentFilter = newFilter
  };


</script>

<style>
  .container {
    max-width: 800px;
    margin: 10px auto;
  }
  .logo {
    display: block;
    margin: 20px auto;
    width: 50%;
  }
  .todo-input {
    width: 100%;
    padding: 10px, 20px;
    font-size: 18px;
    margin-bottom: 20px;
  }
  .inner-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 15px;
    margin-bottom: 13px;
  }
  .inner-container-input {
    margin-right: 12px;
  }
  button {
    font-size: 14px;
    background-color: white;
    appearance: none;
  }
  button:hover {
    background: lightseagreen;
    color: white;
  }
  button:focus {
    outline: none;
  }
  /* .active {
        background: lightseagreen;
    } */
</style>

<div class="container">

  <img class="logo" src={'/img/CTSWLogo.png'} alt="CodingTheSmartWay Logo" />

  <h2>Svelte Todo App</h2>
  <input
    type="text"
    class="todo-input"
    placeholder="Insert todo item ..."
    bind:value={newTodoTitle}
    on:keydown={addTodo} />

  {#each filteredTodos as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleToggleComplete} />
    </div>
  {/each}

  <div class="inner-container">
    <div>
      <label>
        <input class="inner-container-input" type="checkbox" on:change={checkAllTodos}/>
        Check All
      </label>
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <button on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">All</button>
      <button on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">Active</button>
      <button on:click={() => updateFilter('completed')} class:active="{currentFilter === 'completed'}">Completed</button>
    </div>
    <dir>
      <button on:click={clearCompleted}>Clear Completed</button>
    </dir>
  </div>

</div>