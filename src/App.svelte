<script>
  import { onMount } from 'svelte';

  let formFields = [];
  let formData = {};

  async function fetchFormFields() {
    try {
      const response = await fetch('https://api.recruitly.io/api/job?apiKey=TEST64518616D4CF145D4E20BD47169EA7229BA3');
      formFields = await response.json();
    } catch (error) {
      console.error(error);
    }
  }

  async function submitForm() {
    try {
      const response = await fetch('https://api.recruitly.io/api/job?apiKey=TEST64518616D4CF145D4E20BD47169EA7229BA3', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      });
      // Handle the response as needed
    } catch (error) {
      console.error(error);
    }
  }

  onMount(fetchFormFields);
</script>

<main>
  {#if formFields.length > 0}
    <form on:submit|preventDefault={submitForm}>
      {#each formFields as field}
        <label for={field.name}>{field.label}</label>
        {#if field.type === 'text'}
          <input type="text" id={field.name} name={field.name} bind:value={formData[field.name]} />
        {:else if field.type === 'checkbox'}
          <input type="checkbox" id={field.name} name={field.name} bind:checked={formData[field.name]} />
        {:else if field.type === 'select'}
          <select id={field.name} name={field.name} bind:value={formData[field.name]}>
            {#each field.options as option}
              <option value={option}>{option}</option>
            {/each}
          </select>
        {/if}
      {/each}
      <button type="submit">Submit</button>
    </form>
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

  input,
  select {
    padding: 0.5rem;
    margin-bottom: 1rem;
    width: 300px;
  }

  button {
    padding: 0.5rem 1rem;
  }
</style>
