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

<style>
form {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
input {
  width: 80%;
  padding: 8px;
  font-size: 16px;
}
button {
  width: 18%;
  padding: 8px;
  font-size: 16px;
}
</style>
