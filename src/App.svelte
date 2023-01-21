<script>
  import Todos from "./components/Todos.svelte";

  let todos = [
    { id: 1, name: "Create a Svelte starter app", completed: true },
    { id: 2, name: "Set up the svelte, learn about reactivity", completed: true },
    { id: 3, name: "Make it look good", completed: true },
    { id: 4, name: "Componentize everything", completed: true },
    { id: 5, name: "Local storage bitch", completed: false },
    { id: 6, name: "Read about arrow functions: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions", completed: false },
    { id: 7, name: "Responsive", completed: false },
    { id: 8, name: "Accessibility: https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_reactivity_lifecycle_accessibility#exploring_keyboard_accessibility_issues_in_our_to-do_app", completed: false },

  ];

</script>

<main>
  <Todos {todos}/>
</main>