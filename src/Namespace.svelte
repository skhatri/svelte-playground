<script>
  import { onMount } from "svelte";
  import { namespaceStore } from "./namespace_store.js";

  export let title;
  export let className;
  let namespaces = [];
  onMount(async () => {
    const res = await fetch("http://localhost:6100/api/namespaces");
    let responseData = await res.json();
    namespaces = [...responseData.data.namespaces, "any"];
  });
  function selectNamespace(ns) {
    namespaceStore.set(ns);
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
      {title}
      <span class="badge badge-dark">{namespaces.length}</span>
    </div>
    <div class="card-body">
      <ul>
        {#each namespaces as ns}
          <li>
            <a href="#" on:click={selectNamespace(ns)}>
              <span class="badge badge-light">{ns}</span>
            </a>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</main>
