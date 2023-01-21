<script>
  // create a variable that defaults to all
  export let filter
  
  // declares the "hit" handler prop as a dummy fore errors
  // reactive statemenet so that when "filter" value changes, the component updates the filter
  // export let hit = (selected) => {}
  // $: hit(filter)
  // okay wait no longer necessary with bind:filter

  // this function takes that variable and depending on its value will filter the array accordingly
  // the function synta returns the array after it's filtered
  const filterTodos = (filter, todos) =>
    filter === 'left' ? todos.filter((t) => !t.completed) :
    filter === 'completed' ? todos.filter((t) => t.completed) :
    todos
</script>

<div class="filters">
  <button 
    class="btn toggle-btn" 
    class:btn__selected={filter === 'all'} 
    aria-pressed={filter === 'all'} 
    on:click={() => filter = 'all'} >
    <span>All</span>
  </button>
  <button 
    class="btn toggle-btn" 
    class:btn__selected={filter === 'left'} 
    aria-pressed={filter === 'left'} 
    on:click={() => filter = 'left'}>
    <span>Left</span>
  </button>
  <button 
    class="btn toggle-btn" 
    class:btn__selected={filter === 'completed'} 
    aria-pressed={filter === 'completed'} 
    on:click={() => filter = 'completed'}>
    <span>Completed</span>
  </button>
</div>