<script lang="ts">
  const clientId = import.meta.env.VITE_STRAVA_CLIENT_ID;
  const redirectUri = encodeURIComponent(import.meta.env.VITE_REDIRECT_URI || '');
  const scopes = "read,activity:read";
  
  function connectStrava() {
    const authUrl = `https://www.strava.com/oauth/authorize?client_id=${clientId}&response_type=code&redirect_uri=${redirectUri}&approval_prompt=auto&scope=${scopes}`;
    window.location.href = authUrl;
  }
</script>

<svelte:head>
  <title>Connect Strava</title>
</svelte:head>

<main class="container">
  <h1>Connect Your Strava Account</h1>
  <button on:click={connectStrava}>Connect with Strava</button>
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

  h1 {
    margin-bottom: 2rem;
  }

  button {
    padding: 0.75rem 1.5rem;
    font-size: 1.2rem;
    background-color: #FC4C02;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  button:hover {
    background-color: #E34402;
  }
</style>