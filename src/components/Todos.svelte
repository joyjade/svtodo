<script>
  import FilterMenu from "./FilterMenu.svelte";
  import TodoStatus from "./TodoStatus.svelte";
  import Todo from "./Todo.svelte";
  import MoreActions from "./MoreActions.svelte";

  export let todos = []

  $: totalTodos = todos.length;
  $: completedTodos = todos.filter((todo) => todo.completed).length;

  let newTodoName = ''
  let newTodoId
    $: {
      if (totalTodos == 0) {
        newTodoId = 1;
      } else {
        newTodoId = Math.max(...todos.map((t) => t.id)) + 1;
      }
    }

  function removeTodo(todo) {
    todos = todos.filter((td) => td.id !== todo.id)
  }

  function addTodo(todo) {
    todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }]
    newTodoName = ''
  }

  function updateTodo(todo) {
    const index = todos.findIndex((t) => t.id === todo.id)
    todos[index] = {...todos[index], ...todo}
  }
  
  let filter = 'all'
  // this function takes that variable and depending on its value will filter the array accordingly
  // the function synta returns the array after it's filtered
  const filterTodos = (filter, todos) =>
    filter === 'left' ? todos.filter((t) => !t.completed) :
    filter === 'completed' ? todos.filter((t) => t.completed) :
    todos


  const checkAllTodos = (completed) => {
    todos = todos.map((t) => ({ ...t, completed }));
  }

  const removeCompletedTodos = () => todos = todos.filter((td) => !td.completed);
</script>

<div class="todoapp stack-large">
  <h1 class="label-wrapper">
    <label for="todo-0" class="label__lg"> Silly things required of the day </label>
  </h1>

  <!-- FilterMenu: takes in the value of the filter, and passes it an event handler: "()=>{}" as the prop "hit"
    child baby will execute "hit" which will modiy the parent's state
    okay but binding just means propogates the event from the child back to the parent-->
  <div class="flex subheader">
    <FilterMenu bind:filter/>
    <TodoStatus {completedTodos} {totalTodos} />
  </div>
    
  <!-- NewTodo -->
  <form on:submit|preventDefault={addTodo}>
    <div class="flex">
      <input bind:value={newTodoName} type="text" id="todo-0" autocomplete="off" class="input input__lg" />
      <button type="submit" disabled="" class="btn btn__primary btn__lg">
        Add
      </button>
    </div>
  </form>

  <ul role="list" class="todo-list" aria-labelledby="list-heading">  
      {#each filterTodos(filter, todos) as todo (todo.id)}
        <li class="todo">
          <Todo {todo} 
            on:update={(e) => updateTodo(e.detail)}
            on:remove={((e) => {removeTodo(e.detail)})
          }/>
        </li>
      {:else}
        <li>Nothing to do here</li>
      {/each}
  </ul>

  <MoreActions {todos}
    on:checkAll={(e) => checkAllTodos(e.detail)}
    on:removeCompleted={removeCompletedTodos}
    />

</div>
