<script>
  import Library from './library/Library.svelte';
  import Detail from './detail/Detail.svelte';

  let page = 'library';
  let pageArgs = {};

  function bookSelected (event) {
    page = 'detail';
    pageArgs = event.detail;
  }
</script>

<main>
  {#if page === 'detail'}
    <Detail { ...pageArgs } />
  {:else}
    <Library on:book-select={ bookSelected } />
  {/if}
</main>

<style>
  main {
    padding: var(--spacingLarge);
  }
</style>