<script>
  import Fractal from "./Fractal.svelte";
</script>

<div class="all">
  <div class="above">
    <h1>App</h1>
  </div>

  <div class="main">
    <Fractal />
  </div>
</div>

<style>
  .all {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: rgba(0.2, 0.2, 0.2, 0.2);
    border: 2px dotted yellowgreen;
  }

  .above {
    background-color: green;
    margin: 5px;
    padding: 5px;
  }

  .main {
    background-color: #311;
    padding: 10px;
    margin: 5px;
    border: 2px dotted yellowgreen;
  }

  h1 {
    background-color: red;
  }
</style>
