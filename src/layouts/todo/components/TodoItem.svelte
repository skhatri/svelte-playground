<script>
  import { createEventDispatcher } from "svelte";
  import { todoEvent } from "../stores/todo_stores.js";
  export let item = {};
  export let edit;
  let feedback;

  async function update() {
    const result = await fetch(`http://localhost:8080/todo/${item.id}`, {
      method: "POST",
      mode: "cors",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(item)
    })
      .then(res => res.json())
      .then(responseData => responseData.data)
      .catch(err => {
        feedback = err;
      });
    if (result && result.id) {
      feedback = `Updated Task ${result.id}`;
      todoEvent.set({ action: "UPDATED", id: result.id });
      description = "";
      status = "";
      action_by = "";
    }
    console.log(result);
  }
  function cancel() {
    edit = false;
  }
  const dispatch = createEventDispatcher();
</script>

{#if edit}
  <tr>
    <td colspan="6">
      <form class="form-inline">
        <div class="form-group mb-2">
          <label for="description">
            <span>Task</span>
            &nbsp;
          </label>
          <input type="hidden" id="id" bind:value={item.id} />
          <input
            type="text"
            class="form-control"
            id="description"
            bind:value={item.description}
            placeholder="Description..." />
          &nbsp;
        </div>
        <div class="form-group mb-2">
          <input
            type="text"
            class="form-control"
            id="action_by"
            bind:value={item.action_by}
            placeholder="Action By" />
          &nbsp;
        </div>
        <div class="form-group mb-2">
          <input
            type="text"
            class="form-control"
            id="status"
            bind:value={item.status}
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
    <td>{item.description}</td>
    <td>{item.action_by}</td>
    <td>{item.status}</td>
    <td>{item.created}</td>
    <td>{item.updated}</td>
    <td>
      <a href="#" on:click={() => dispatch('edit', item.id)}>
        <span class="oi oi-pencil" />
      </a>
      <a href="#" on:click={() => dispatch('remove', item.id)}>
        <span class="oi oi-trash" />
      </a>
    </td>
  </tr>
{/if}
