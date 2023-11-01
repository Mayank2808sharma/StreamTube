<script>
    import { createEventDispatcher } from 'svelte';
    import { Form, FormGroup, FormText, Input, Label } from 'sveltestrap';
    const dispatch = createEventDispatcher();
    let searchTerm = '';
  
    const search = () => {
      dispatch('click', { searchTerm });
    };
  </script>
  
  <form on:submit|preventDefault={search}>
    <FormGroup>
        <Label for="exampleText">Text</Label>
        <Input id="exampleText" value="Some text value" />
    </FormGroup>
    <input bind:value={searchTerm} placeholder="Search..." />
    <button type="submit">Search</button>
  </form>
  