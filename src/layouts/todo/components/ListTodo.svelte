<script>
  import { createEventDispatcher, onMount } from "svelte";
  import TodoItem from "./TodoItem.svelte";
  import { todoEvent } from "../stores/todo_stores.js";

  let items = [];
  let feedback = "";

  async function editTodo(item) {
    console.log(`edit ${item.payload.id}`);
    item.edit = true;
    const data = await fetch(`http://localhost:8080/todo/${item.payload.id}`)
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    if (data) {
      todoEvent.set({ action: "EDIT", data });
    }
  }

  async function removeTodo(item) {
    console.log(`remove ${item.payload.id}`);
    const data = await fetch(`http://localhost:8080/todo/${item.payload.id}`, {
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
      todoEvent.set({ action: "DELETED", id: item.payload.id });
    }
  }

  async function fetchTodoList() {
    const data = await fetch(`http://localhost:8080/todo/search`)
      .then(res => res.json())
      .then(responseData => responseData.data)
      .then(data => {
        return data.map(item => {
          return {
            payload: item,
            edit: false
          };
        });
      })
      .catch(err => {
        feedback = err;
      });
    items = data;
  }
  todoEvent.subscribe(ev => {
    if (
      ev &&
      ev.action &&
      (ev.action === "DELETED" ||
        ev.action === "UPDATED" ||
        ev.action === "ADDDED")
    ) {
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
          on:edit={e => editTodo(it)}
          on:remove={e => removeTodo(it)} />
      {/each}
    </tbody>
  </table>
</main>
