<script>
  export let name;
  import { Router, Route } from "svelte-routing";

  import Navigation from "./components/Navigation.svelte";
  import K8sReaderComponent from "./views/K8sReaderComponent.svelte";
  import LocalWidgetsComponent from "./views/LocalWidgetComponent.svelte";
  import TodoComponent from "./views/TodoComponent.svelte";
</script>

<style>
  h1 {
    color: #ff3e00;
    font-size: 3em;
    font-weight: 100;
  }
</style>

<main>
  <div class="container-fluid w-100">
    <Router>

      <Navigation />
      <h1>{name}</h1>

      <div class="container-fluid w-100">
        <Route path="/" component={K8sReaderComponent} />
        <Route path="/todo" component={TodoComponent} />
        <Route path="/widgets" component={LocalWidgetsComponent} />
      </div>
    </Router>
  </div>
</main>
