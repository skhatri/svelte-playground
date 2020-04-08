<script>
  import { todoEvent } from "../stores/todo_stores.js";

  export let description = "";
  export let action_by = "";
  export let status = "";
  export let id = "";

  let feedback;

  async function addTodo() {
    let item = {
      id: id,
      created: "",
      updated: "",
      description: description,
      action_by: action_by,
      status: status
    };
    const result = await fetch(`http://localhost:8080/todo/`, {
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
      feedback = `Added Task ${result.id}`;
      todoEvent.set({ action: "ADD", id: result.id });
      description = "";
      status = "";
      action_by = "";
    }
    console.log(result);
  }
</script>

<main>
  <form class="form-inline">
    <div class="form-group mb-2">
      <label for="description">
        <span class="font-weight-bold">Task</span>
        &nbsp;
      </label>
      <input
        type="text"
        class="form-control"
        id="description"
        bind:value={description}
        placeholder="Description..." />
      &nbsp;
    </div>
    <div class="form-group mb-2">
      <input
        type="text"
        class="form-control"
        id="action_by"
        bind:value={action_by}
        placeholder="Action By" />
      &nbsp;
    </div>
    <div class="form-group mb-2">
      <input
        type="text"
        class="form-control"
        id="status"
        bind:value={status}
        placeholder="Status" />
      &nbsp;
    </div>
    &nbsp;
    <button
      id="add-button"
      class="btn btn-primary mb-2"
      type="button"
      on:click={addTodo}>
      Add
    </button>
  </form>
  {#if feedback}
    <div class="alert alert-info">{feedback}</div>
  {/if}
</main>
