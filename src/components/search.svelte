<script>
  import {createEventDispatcher} from 'svelte';
  const dispatch = createEventDispatcher();
  export let searchTerm;
</script>

<div class="wrapper">
  <h4>Search {#if searchTerm}for <span class="searchValue">{searchTerm}</span>{/if}</h4>
  <div class="form">
    <input class="input" type="text" 
      bind:value={searchTerm} 
      on:keyup={() => {dispatch("updateSearch");}}/>
    <button class="button" 
      on:click={() => dispatch('resetSearch')}>Clear</button>
  </div>
</div>

<style>
  .wrapper {
    padding-top: 1rem;
  }
  .searchValue {
    color: var(--primary);
  }
  .form {
    display: flex;
    flex-direction: row;
    gap: 1rem;
  }
  .input {
    width: 75%;
  }
  .button {
    width: 25%;
  }
</style>