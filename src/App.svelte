<script>
  import Library from './library/Library.svelte';

  function bookSelected (event) {
    console.warn('book clickeD: ', event.detail.bookId);
  }
</script>

<main>
  <Library on:book-select={ bookSelected } />
</main>

<style>
</style>