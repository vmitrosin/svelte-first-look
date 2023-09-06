<script>
	import { onMount } from 'svelte';
  import Post from '../components/post.svelte';
  import Search from '../components/search.svelte';
  let posts = [];
  let displayPosts = [];
  let searchTerm = '';

  onMount(async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts = await response.json();
    displayPosts = posts;
  });

  function filterList(list, query) {
    return list.filter(item => {
      return item.title.toLowerCase().match(query.toLowerCase());
    });
  }
</script>

<div class="container">
  <Search 
    bind:searchTerm
    on:updateSearch = {() => {
      displayPosts = filterList(posts, searchTerm);
    }}
    on:resetSearch = {() => {
      searchTerm = '';
      displayPosts = posts;
    }}
  />

  {#each displayPosts as post}
    <Post bind:title={post.title} body={post.body}/>
    {:else}
    <p>No data to display</p>
  {/each}
</div>


