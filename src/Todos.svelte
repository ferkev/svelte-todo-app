<script>
  import TodoItem from './TodoItem.svelte';

  let Todos = [
    {
      id: 1,
      title: "Create a symphony",
      description: "be a new music artist and make some noise",
      completed: false
    },
    {
      id: 2,
      title: "Make a svelte presentation",
      description: "elaborate a new presentation of the famous svelte framework",
      completed: true
    },
    {
      id: 3,
      title: "Be happy",
      description: "Don't worry be happy now",
      completed: false
    }
  ]

  let newTodoTitle = '';
  let currentFilter = 'all';
  let nextId = Todos.length + 1;

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
    }
    button:focus {
        outline: none;
    }
    /* .active {
        background: lightseagreen;
    } */
</style>

<div class="container">
    
    <img class="logo" src={'/img/CTSWLogo.png'} alt="CodingTheSmartWay Logo">
    
    <h2>Svelte Todo App</h2>
    
    <input type="text" class="todo-input" placeholder="Insert todo item ...">
    
    <div class="todo-item"></div>

    <div class="inner-container">
      <div><label><input class="inner-container-input" type="checkbox">Check All</label></div>
      <div>items left</div>
    </div>

    <div class="inner-container">
        <div>
            <button>All</button>
            <button>Active</button>
            <button>Completed</button>
        </div>
        <dir>
            <button>Clear Completed</button>
        </dir>
    </div>

</div>