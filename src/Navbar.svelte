<script>
  export let handleShowForm;
</script>
<nav class="nav">
    <div class="nav-center">
      <h1 class="nav-title">Budget Calculator</h1>
    </div>
    <button type="button" class="nav-btn" on:click={handleShowForm}>
      <i class="far fa-plus-square" />
      add item
    </button>
  </nav>
  