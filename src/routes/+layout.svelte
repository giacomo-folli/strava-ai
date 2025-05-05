<script lang="ts">
  import { onMount } from "svelte";
</script>

<svelte:head>
  <title>Strava Connection</title>
</svelte:head>

<main class="container">
  <slot />
</main>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    font-family: system-ui, sans-serif;
  }

  :global(h1) {
    margin-bottom: 2rem;
    text-align: center;
    max-width: 600px;
    padding: 0 1rem;
  }

  :global(button) {
    padding: 0.75rem 1.5rem;
    font-size: 1.2rem;
    background-color: #fc4c02;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  :global(button:hover) {
    background-color: #e34402;
  }
</style>
