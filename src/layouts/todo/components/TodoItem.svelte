<script>
  import { createEventDispatcher, onMount } from "svelte";

  import { todoEvent } from "../stores/todo_stores.js";
  export let item = {};
  let feedback;
  let originalCopy;

  async function update() {
    var updateItem = {
      id: item.payload.id,
      description: item.payload.description,
      action_by: item.payload.action_by,
      status: item.payload.status
    };
    const result = await fetch(
      `http://localhost:8080/todo/${item.payload.id}`,
      {
        method: "POST",
        mode: "cors",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(updateItem)
      }
    )
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    if (result && result.id) {
      feedback = `Updated Task ${result.id}`;
      todoEvent.set({ action: "UPDATED", id: result.id });
    }
  }
  function cancel() {
    item.edit = false;
    item.payload = JSON.parse(originalCopy);
  }
  const dispatch = createEventDispatcher();
  todoEvent.subscribe(evt => {
    item.edit = evt.action === "EDIT" && evt.data.id === item.payload.id;
    if (item.edit) {
      originalCopy = JSON.stringify(item.payload);
    }
  });
</script>

{#if item.edit}
  <tr>
    <td colspan="6">
      <form class="form-inline">
        <div class="form-group mb-2">
          <label for="description">
            <span>Task</span>
            &nbsp;
          </label>
          <input type="hidden" id="id" bind:value={item.payload.id} />
          <input
            type="text"
            class="form-control"
            id="description"
            bind:value={item.payload.description}
            placeholder="Description..." />
          &nbsp;
        </div>
        <div class="form-group mb-2">
          <input
            type="text"
            class="form-control"
            id="action_by"
            bind:value={item.payload.action_by}
            placeholder="Action By" />
          &nbsp;
        </div>
        <div class="form-group mb-2">
          <input
            type="text"
            class="form-control"
            id="status"
            bind:value={item.payload.status}
            placeholder="Status" />
          &nbsp;
        </div>
        &nbsp;
        <button
          id="add-button"
          class="btn btn-primary mb-2"
          type="button"
          on:click={update}>
          Update
        </button>
        &nbsp;
        <button
          id="add-button"
          class="btn btn-secondary mb-2"
          type="button"
          on:click={cancel}>
          Cancel
        </button>
      </form>
      {#if feedback}
        <div class="alert alert-info">{feedback}</div>
      {/if}
    </td>
  </tr>
{:else}
  <tr>
    <td>{item.payload.description}</td>
    <td>{item.payload.action_by}</td>
    <td>{item.payload.status}</td>
    <td>{item.payload.created}</td>
    <td>{item.payload.updated}</td>
    <td>
      <a href="#" on:click={() => dispatch('edit', item.payload.id)}>
        <span class="oi oi-pencil" />
      </a>
      <a href="#" on:click={() => dispatch('remove', item.payload.id)}>
        <span class="oi oi-trash" />
      </a>
    </td>
  </tr>
{/if}
