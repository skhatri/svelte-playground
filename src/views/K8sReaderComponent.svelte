<script>
  import Namespace from "../Namespace.svelte";
  import Workload from "../Workload.svelte";
</script>

<main>
  K8sReaderComponent
  <div class="container-fluid w-100">
    <div class="row w-100">
      <div class="col-sm-4">
        <Namespace title="Namespaces" className="alert alert-info" />
      </div>
    </div>
    <div class="row w-100">
      <div class="col-sm-4">
        <Workload
          title="Jobs"
          objectType="jobs"
          className="alert alert-primary" />
      </div>

      <div class="col-sm-4">
        <Workload
          title="Deployments"
          objectType="deployments"
          className="alert alert-success" />
      </div>
      <div class="col-sm-4">
        <Workload
          title="Statefulsets"
          objectType="statefulsets"
          className="alert alert-warning" />
      </div>
    </div>
  </div>
</main>
