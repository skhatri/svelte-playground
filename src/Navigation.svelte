<script>
  import { Link } from "svelte-routing";
</script>

<main>
  <nav class="navbar navbar-expand-lg navbar-light bg-light w-100">
    <a class="navbar-brand" href="#">K8S Dashboard</a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarNavAltMarkup"
      aria-controls="navbarNavAltMarkup"
      aria-expanded="false"
      aria-label="K8S Dashboard">
      <span class="navbar-toggler-icon" />
    </button>
    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div class="navbar-nav">
        <Link to="/" class="nav-item nav-link active" href="#">
          K8s
          <span class="sr-only">(current)</span>
        </Link>
        <Link to="/widgets" class="nav-item nav-link" href="#">Widgets</Link>
        <Link to="/todo" class="nav-item nav-link disabled" href="#">TODO</Link>
      </div>
    </div>
  </nav>
</main>
