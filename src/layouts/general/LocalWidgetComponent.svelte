<script>
  import Fibonacci from "./components/Fibonacci.svelte";
  import Counter from "./components/Counter.svelte";
</script>

<main>
  <div class="container-fluid w-100">
    <div class="row w-100">
      <div class="col-sm-4">
        <Fibonacci title="Fibonacci" num="0" />
      </div>
      <div class="col-sm-4">
        <Counter title="Counter" data="Counter Values" count="2" />
      </div>
    </div>
  </div>
</main>
