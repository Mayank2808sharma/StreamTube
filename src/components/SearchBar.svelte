<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    let searchTerm = '';
  
    const search = () => {
      dispatch('click', { searchTerm });
    };
  </script>
  
  <form on:submit|preventDefault={search}>
    <input bind:value={searchTerm} placeholder="Search..." />
    <button type="submit">Search</button>
  </form>
  