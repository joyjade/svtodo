<script>
  import { createEventDispatcher } from "svelte";
  import Todos from "./Todos.svelte";
  const dispatch = createEventDispatcher();

  export let todos;
  let completed = true;

  const checkAll = () => {
    dispatch("checkAll", completed);
    completed = !completed;
  }
  const removeCompleted = () => dispatch('removeCompleted');

  $: completedTodos = todos.filter((t) => t.completed).length
</script>

  <div class="btn-group more-actions">
    <button type="button" class="btn btn__primary" on:click={checkAll}>
      {completed ? 'Check' : 'Uncheck'} all</button>
      <button type="button" class="btn btn__primary" disabled={completedTodos === 0} on:click={removeCompleted}>Remove completed</button>
  </div>