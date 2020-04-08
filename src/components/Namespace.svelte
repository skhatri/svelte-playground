<script>
  import { onMount } from "svelte";
  import { namespaceStore } from "../stores/namespace_store.js";

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

</style>

<main>
  <div class="container-fluid">
    <ul class="nav nav-pills">
      {#each namespaces as ns}
        <li class="nav-item">
          <a class="nav-link" href="#" on:click={selectNamespace(ns)}>{ns}</a>
        </li>
      {/each}
    </ul>
  </div>
</main>
