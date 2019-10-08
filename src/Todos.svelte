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
  let nextId = 4;

  /**
   * @desc: function for adding task
   * @param: {event} e - the event when keydown enter is down
   **/
  const addTodo = e => {
    if (e.key === "Enter") {
      todos = [
        ...todos,
        {
          id: nextId,
          title: newTodoTitle,
          completed: false
        }
      ];
      nextId += 1;
      newTodoTitle = "";
    }
  };

  /**
   * @desc: function to change the filter option
   * @param: {string} newFilter - a filter to execute the selection
   * @return: {string} currentFilter - the new filter choosen
   **/
  const updateFilter = newFilter => {
    currentFilter = newFilter;
  };

  /**
   * @desc: function
   * @param: {event} e - check event
   **/
  const checkAllTodos = e => {
    todos.forEach(todo => todo.completed = e.target.checked);
    todos = todos;
  };

  /**
   * @desc: clear completed tasks
   **/
  const clearCompleted = () => {
    todos = todos.filter(todo => !todo.completed);
  };

  /**
   * @desc: delete task which are completed
   * @param: {event} e - event on click
   **/
  const handleDeleteTodo = e => {
    todos = todos.filter(todo => todo.id !== e.detail.id);
  };

  /**
   * @desc: complete task are displaying completed
   * @param: {event} e - event on click
   **/
  const handleToggleComplete = e => {
    // find todo index
    const todoIndex = todos.findIndex(todo => {
      return todo.id === e.detail.id;
    });

    // actualize the todos array
    const updatesTodo = {...todos[todoIndex], completed: !todos[todoIndex].completed};
    todos = [
      ...todos.slice(0, todoIndex),
      updatesTodo,
      ...todos.slice(todoIndex + 1)
    ];
  };

  // update the dom for remaining task count
  $: todosRemaining = filteredTodos.filter(todo => !todo.completed).length;

  // filter for displaying todos
  $: filteredTodos = currentFilter === "all" ? todos : currentFilter === "completed"
      ? todos.filter(todo => todo.completed)
      : todos.filter(todo => !todo.completed);
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
  .active {
    background: lightseagreen;
  }
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
        <input
          class="inner-container-input"
          type="checkbox"
          on:change={checkAllTodos} />
        Check All
      </label>
    </div>
    <div>{todosRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <button
        on:click={() => updateFilter('all')}
        class:active={currentFilter === 'all'}>
        All
      </button>
      <button
        on:click={() => updateFilter('active')}
        class:active={currentFilter === 'active'}>
        Active
      </button>
      <button
        on:click={() => updateFilter('completed')}
        class:active={currentFilter === 'completed'}>
        Completed
      </button>
    </div>
    <dir>
      <button on:click={clearCompleted}>Clear Completed</button>
    </dir>
  </div>

</div>
