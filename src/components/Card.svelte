<script>
  export let title;
  export let data;
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
    <div class="card-body">{data}</div>
  </div>
</main>
