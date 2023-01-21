<script>
  import Todos from "./components/Todos.svelte";

  let todos = [
    { id: 1, name: "Create a Svelte starter app", completed: true },
    { id: 2, name: "Set up the svelte, learn about reactivity", completed: true },
    { id: 3, name: "Make it look good", completed: false },
    { id: 4, name: "Componentize everything", completed: true },
    { id: 5, name: "Local storage bitch", completed: false },
    { id: 6, name: "Read about arrow functions: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions", completed: false }
  ];

</script>

<main>
  <Todos {todos}/>
</main>