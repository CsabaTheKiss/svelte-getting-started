<script>
  import { navigate } from 'svelte-routing'; 
  import BackButtonRow from '../common/BackButtonRow.svelte';
  import BookCover from '../common/BookCover.svelte';
  import Button from '../common/Button.svelte';
  import Header from '../common/Header.svelte';
  import TextInput from '../common/TextInput.svelte';

  import { httpPost } from '../common/api.js';

  let bookDetails = {
    title: '',
    author: '',
    cover: '',
    about: ''
  }

  // $: called each time the component has a change
  // here 'coverBookDetails' will be re-calculated every time, while an input field value below changes
  $: coverBookDetails = { ...bookDetails };

  async function handleSubmit (event) {
    const newBook = {
      ...coverBookDetails,
      variation: getRandomInt(0, 2),
      favorite: false
    }

    const { ok } = await httpPost('/', newBook);
    if (ok) {
      navigate('/');
    }
  }

  function getRandomInt(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }

</script>

<BackButtonRow />

<Header element="h1" size="large">Create</Header>
<!-- event modifier: |preventDefault -->
<form on:submit|preventDefault={ handleSubmit }>
  <div class="fields">
    <TextInput label="Title" bind:value={bookDetails.title} />
    <TextInput label="Author" bind:value={bookDetails.author} />
    <TextInput label="Cover URL" bind:value={bookDetails.cover} />
    <TextInput label="About" multiline bind:value={bookDetails.about} />
  </div>

  <div>
    <Header>Preview</Header>
    <div class="preview">
      <BookCover book={coverBookDetails}/>
    </div>
  </div>
  <div>
    <Button>Save</Button>
  </div>
</form>


<style>
  form {
    display: grid;
    grid-auto-rows: auto;
    grid-template-columns: 1fr;
    gap: var(--spacingXLarge);
  }
  .fields {
    display: grid;
    grid-auto-rows: auto;
    gap: var(--spacingMedium);
  }
  .preview {
    display: grid;
    grid-template-columns: minmax(20vw, 10rem);
    grid-template-rows: minmax(32vw, 16rem);
  }
  @media (min-width: 48rem) {
    form {
      grid-template-columns: 60vw 20vw;
    }
  }
</style>
