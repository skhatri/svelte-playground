<script>
  import { onMount } from "svelte";
  import { namespaceStore } from "./namespace_store.js";

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
</style>

<main>
  <div class="card border-primary {className}" style="height: 17rem;">
    <div class="card-header">
      {title} - {current_namespace}
      <span class="badge badge-dark">{items.length}</span>
    </div>
    <div class="card-body">
      <ul>
        {#each items as item}
          <li>
            <span class="badge badge-info">{item.name}</span>
            <span class="badge badge-light">{item.image}</span>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</main>
