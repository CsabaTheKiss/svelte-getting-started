<script>
  import Library from './library/Library.svelte';

  function bookClickedHandler (bookId) {
    console.warn('book clickeD: ', bookId);
  }
</script>

<main>
  <Library onBookSelect={ bookClickedHandler } />
</main>

<style>
</style>