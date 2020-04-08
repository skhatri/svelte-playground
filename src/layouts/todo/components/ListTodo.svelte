<script>
  import { createEventDispatcher, onMount } from "svelte";
  import TodoItem from "./TodoItem.svelte";
  import { todoEvent } from "../stores/todo_stores.js";

  let status = "";
  let items = [];
  let feedback = "";
  let editId = "";

  async function editTodo(id) {
    console.log(`edit ${id}`);
    const data = await fetch(`http://localhost:8080/todo/${id}`)
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    if (data) {
      editId = data.id;
      todoEvent.set({ action: "EDIT", data });
    }
  }

  async function removeTodo(id) {
    console.log(`remove ${id}`);
    const data = await fetch(`http://localhost:8080/todo/${id}`, {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json"
      }
    })
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    if (data) {
      editId = "";
      todoEvent.set({ action: "DELETE", id: id });
    }
  }

  async function fetchTodoList() {
    const data = await fetch(`http://localhost:8080/todo/search`)
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    editId = "";
    items = data;
  }
  todoEvent.subscribe(ev => {
    if (ev && ev.id) {
      console.log(ev);
      fetchTodoList();
    }
  });
  onMount(() => fetchTodoList());
</script>

<main>
  {#if feedback}
    <div class="alert alert-info">{feedback}</div>
  {/if}
  <table class="table table-striped">
    <thead>
      <tr>
        <th>Description</th>
        <th>Action By</th>
        <th>Status</th>
        <th>Created</th>
        <th>Updated</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      {#each items as it}
        <TodoItem
          item={it}
          edit={it.id == editId}
          on:edit={e => editTodo(it.id)}
          on:remove={e => removeTodo(it.id)} />
      {/each}
    </tbody>
  </table>
</main>
