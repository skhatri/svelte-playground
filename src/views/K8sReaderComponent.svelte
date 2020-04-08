<script>
  import Namespace from "../components/Namespace.svelte";
  import Workload from "../components/Workload.svelte";
</script>

<main>

  <div class="container-fluid w-100">
    <div class="row">
      <div class="col-sm-4">&nbsp;</div>
    </div>
    <div class="row w-100">
      <div class="w-100">
        <Namespace title="Namespaces" className="alert alert-info" />
      </div>
    </div>
    <div class="row w-100">
      <div class="col-sm-4">
        <Workload
          title="Deployments"
          objectType="deployments"
          className="alert alert-primary" />
      </div>
      <div class="col-sm-4">
        <Workload
          title="Statefulsets"
          objectType="statefulsets"
          className="alert alert-warning" />
      </div>
      <div class="col-sm-4">
        <Workload
          title="Jobs"
          objectType="jobs"
          className="alert alert-success" />
      </div>

    </div>
  </div>
</main>
