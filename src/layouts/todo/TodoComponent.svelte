<script>
  import ListTodo from "./components/ListTodo.svelte";
  import AddEditTodo from "./components/AddEditTodo.svelte";
  import { todoEvent } from "./stores/todo_stores.js";

  let displayAdd = false;
  function toggleAdd() {
    displayAdd = !displayAdd;
  }
</script>

<style>
  .add {
    font-size: 1rem;
  }
</style>

<main>

  <div class="container-fluid" w-100>

    <div class="container">
      <ListTodo />
      <div>
        <a href="#" on:click={toggleAdd}>
          <span class="oi oi-plus add" />
        </a>
      </div>
      {#if displayAdd}
        <AddEditTodo />
      {/if}
    </div>
  </div>

</main>
