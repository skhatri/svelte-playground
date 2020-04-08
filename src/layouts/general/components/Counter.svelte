<script>
  export let title;

  export let data;
  export let count;
  $: doubled = count * 2;

  function inc() {
    count = parseInt(count) + 1;
  }
  function dec() {
    count = parseInt(count) - 1;
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
  <div class="card border-primary" style="height: 17rem;">
    <div class="card-header">{title}</div>
    <div class="card-body">
      <h3>Count: {count}, Double: {doubled}</h3>
      <div class="btn-group">
        <button class="btn btn-primary" on:click={dec}>-</button>
        <button class="btn">{count}</button>
        <button class="btn btn-secondary" on:click={inc}>+</button>
      </div>

      <p>Counter card</p>
    </div>
  </div>
</main>
