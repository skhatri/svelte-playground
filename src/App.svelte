<script>
  export let name;
  import { Router, Route } from "svelte-routing";

  import Navigation from "./layouts/navigation/Navigation.svelte";
  import K8sReaderComponent from "./layouts/k8s/K8sReaderComponent.svelte";
  import LocalWidgetsComponent from "./layouts/general/LocalWidgetComponent.svelte";
  import TodoComponent from "./layouts/todo/TodoComponent.svelte";
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
        <Route path="/k8s" component={K8sReaderComponent} />
        <Route path="/" component={TodoComponent} />
        <Route path="/widgets" component={LocalWidgetsComponent} />
      </div>
    </Router>
  </div>
</main>
