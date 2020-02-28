<script>
  import TransformExplorer from "./TransformExplorer.svelte";
  import FilterExplorer from "./FilterExplorer.svelte";
</script>

<style lang="scss">
  section {
    scroll-snap-type: y mandatory;
  }
</style>

<main>
  <section>
    <TransformExplorer />
    <FilterExplorer />
  </section>
</main>
