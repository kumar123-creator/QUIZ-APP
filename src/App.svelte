<script>
  import { onMount } from 'svelte';

  let formFields = [];

  onMount(async () => {
    try {
      const response = await fetch('https://api.example.com/form-fields');
      formFields = await response.json();
    } catch (error) {
      console.error(error);
    }
  });
</script>

<main>
  {#if formFields.length > 0}
    <form>
      {#each formFields as field}
        <label for={field.name}>{field.label}</label>
        <input type={field.type} id={field.name} name={field.name} />
      {/each}
      <button type="submit">Submit</button>
    </form>
  {:else}
    <p>Loading form fields...</p>
  {/if}
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  label {
    margin-bottom: 0.5rem;
  }

  input {
    padding: 0.5rem;
    margin-bottom: 1rem;
    width: 300px;
  }

  button {
    padding: 0.5rem 1rem;
  }
</style>
