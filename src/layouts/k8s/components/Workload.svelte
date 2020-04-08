<script>
  import { onMount } from "svelte";
  import { namespaceStore } from "../stores/namespace_store.js";

  export let title;
  export let objectType;
  export let className;
  let items = [];
  onMount(() => fetchData("any"));
  let current_namespace;
  namespaceStore.subscribe(value => {
    current_namespace = value;
    fetchData(current_namespace);
  });

  async function fetchData(namespace_name) {
    const res = await fetch(
      `http://localhost:6100/api/${objectType}?namespace=${namespace_name}`
    );
    let responseData = await res.json();
    items = responseData.data;
  }
</script>

<style>
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  .card-header {
    padding: 0.25rem;
  }
  .card-body {
    padding: 0.25rem;
  }
</style>

<main>
  <div class="card border-secondary" style="min-height: 30rem;">
    <div class="card-header">

      <span class="font-weight-bold">{title} -</span>
      <span class="badge badge-secondary">{current_namespace}</span>
      <span class="badge badge-dark">{items.length}</span>
    </div>
    <div class="card-body w-100">
      {#if items.length > 0}
        <table class="table table-striped table-sm">
          <thead>
            <tr class="table-info">
              <th scope="col">Name</th>
              <th scope="col">Image</th>
              <th scope="col">Replicas</th>
            </tr>
          </thead>
          <tbody>
            {#each items as item}
              <tr>
                <th scope="row">
                  {item.name}
                  <span class="badge badge-secondary">{item.namespace}</span>
                </th>
                <td>{item.image}</td>
                <td>
                  {#if item.replicas > 1}
                    <span class="badge badge-warning badge-pill">
                      {item.replicas}
                    </span>
                  {:else}
                    <span class="badge badge-info badge-pill">
                      {item.replicas}
                    </span>
                  {/if}
                </td>
              </tr>
            {/each}
          </tbody>
        </table>
      {/if}
    </div>
  </div>
</main>
