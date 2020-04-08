<script>
  export let title;
  export let num;
  export let result;

  let _m = {};
  function _fib(c) {
    if (_m[c]) {
      return _m[c];
    }
    let items = new Array(c + 1);
    for (var i = 0; i <= c; i++) {
      if (i == 0) {
        items[i] = 0;
      } else if (i == 1 || i == 2) {
        items[i] = 1;
      } else {
        items[i] = items[i - 2] + items[i - 1];
      }
      _m[i] = items[i];
    }
    return items[c];
  }
  function fibo() {
    result = _fib(num);
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

<link
  rel="stylesheet"
  href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css"
  crossorigin="anonymous" />

<main>

  <div class="card border-primary" style="height: 17rem;">
    <div class="card-header">
      <h3>{title}!</h3>
    </div>
    <div class="card-body">
      <form class="navbar-form pull-left" onsubmit="return false;">
        <input type="text" class="span2" bind:value={num} on:change={fibo} />
        <button class="btn btn-primary" on:click={fibo}>Calculate</button>
      </form>
      <div class="alert alert-primary" role="alert">
        <p>
          Input:
          <span class="badge badge-success">{num}</span>
        </p>
        <p>
          Fibonacci:
          <span class="badge badge-primary">{result}</span>
        </p>

      </div>
    </div>
  </div>

</main>
