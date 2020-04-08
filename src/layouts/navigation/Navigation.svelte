<script>
  import { Link } from "svelte-routing";
</script>

<main>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark w-100">
    <a class="navbar-brand" href="#">Svelte Playground</a>
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
        <Link to="/k8s" class="nav-item nav-link active" href="#">
          <span class="nav-item nav-link">K8s</span>

        </Link>
        <Link to="/widgets" class="nav-item nav-link" href="#">
          <span class="nav-item nav-link">Widgets</span>
        </Link>
        <Link to="/" class="nav-item nav-link disabled" href="#">
          <span class="nav-item nav-link">TODO</span>
        </Link>
      </div>
    </div>
  </nav>
</main>
