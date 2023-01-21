<script>
  import { createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()

  export let todo

  let editing = false
  let name = todo.name // this needs to match the property of the object you're updating

  function update(updatedTodo) {
    todo = {...todo, ...updatedTodo} //applies all the modifications to the todo
    console.log(todo);
    dispatch('update', todo) //dispatch an events with a detail that is an object with a bunch of values
  }

  function onCancel() {
    name = todo.name
    editing = false
  }

  function onSave() {
    update({ name })
    editing = false
  }

  function onRemove() {
    dispatch('remove', todo);
  }

  function onEdit() {
    editing = true
  }

  function onToggle() {
    update({ completed: !todo.completed })
  }
</script>

{#if editing}
  <form on:submit|preventDefault={onSave} on:keydown={(e) => e.key === 'Escape' && onCancel()}>
    <div class="flex row">
      <label for="todo-{todo.id}" class="todo-label"></label>
      <input class="flex item todo-text" bind:value={name} type="text" id="todo-{todo.id}" autocomplete="off" />
      <div class="btn-group">
        <button class="btn todo-cancel" type="button" on:click={onCancel}>
          Cancel
          <span class="visually-hidden">{todo.name}</span>
        </button>
        <button class="btn btn__primary todo-edit" type="submit" on:click={onSave}>
          Save
          <span class="visually-hidden">{todo.name}</span>
        </button>
      </div>
    </div>
  </form>
{:else}
  <div class="flex row">
    <div class="flex item">
      <input type="checkbox" id="todo-{todo.id}" checked={todo.completed} on:click={onToggle}/>
      <label for="todo-{todo.id}" class="todo-label">
        {todo.name}
      </label>
    </div>
    <div class="btn-group">
      <button type="button" class="btn" on:click={onEdit}>
        Edit <span class="visually-hidden">{todo.name}</span>
      </button>
      <button type="button" class="btn btn__danger" on:click={onRemove}>
        Delete <span class="visually-hidden">{todo.name}</span>
      </button>
    </div>
  </div>
{/if}
