<script lang="ts">
  import { onMount } from "svelte";

  let todos = [];

  let currText = "";

  function addTodo() {
    todos = [...todos, currText];
    currText = "";
    updateStorage();
  }

  function removeTodo(text: string) {
    return () => {
      todos = todos.filter((t) => t != text);
      updateStorage();
    };
  }

  function updateStorage() {
    localStorage.setItem("todos", JSON.stringify(todos));
  }

  onMount(() => {
    todos = JSON.parse(localStorage.getItem("todos")) ?? [];
  });
</script>

<main class="flex flex-col justify-start items-center gap-4">
  <h1 class="font-bold text-6xl">Todo Apps</h1>

  <div class="todo-items">
    {#each todos as todo}
      <p on:click={removeTodo(todo)} class="hover:line-through">{todo}</p>
    {/each}
  </div>

  <input type="text" bind:value={currText} class="bg-rose-300 rounded p-2" />

  <button class="bg-blue-400 rounded p-2" on:click={addTodo}>Add Todo</button>

  <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ" target="_blank">
    Click Here
  </a>
</main>

<style lang="postcss">
  :root {
    /*  Meta Font */
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
