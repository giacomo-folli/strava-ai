<script lang="ts">
  import { env } from "$env/dynamic/public";
  import { onMount } from "svelte";

  const scopes = "read,activity:read";
  let email = "";
  let emailError = "";

  function validateEmail(email: string) {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(email);
  }

  function connectStrava() {
    if (!email || !validateEmail(email)) {
      emailError = "Please enter a valid email address";
      return;
    }

    const clientId = env.PUBLIC_VITE_STRAVA_CLIENT_ID;
    const redirectUri = `"${window.location.href}callback?email=${email}"`;

    const queryParams = new URLSearchParams({
      client_id: clientId,
      response_type: "code",
      redirect_uri: redirectUri,
      approval_prompt: "auto",
      scope: scopes,
    });

    const authUrl = `https://www.strava.com/oauth/authorize?${queryParams.toString()}`;

    window.location.href = authUrl;
  }
</script>

<h1>Connect Your Strava Account</h1>

<div class="form-group">
  <label for="email">Email for Activity Updates</label>
  <input
    type="email"
    id="email"
    bind:value={email}
    placeholder="Enter your email"
    on:input={() => (emailError = "")}
  />
  {#if emailError}
    <span class="error">{emailError}</span>
  {/if}
  <p class="note">
    We'll send your activity analysis and coaching tips to this email address.
  </p>
</div>

<button on:click={connectStrava}>Connect with Strava</button>

<style>
  .form-group {
    margin-bottom: 2rem;
    width: 100%;
    max-width: 400px;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 500;
  }

  input {
    width: 100%;
    padding: 0.75rem;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-bottom: 0.5rem;
  }

  input:focus {
    outline: none;
    border-color: #fc4c02;
    box-shadow: 0 0 0 2px rgba(252, 76, 2, 0.1);
  }

  .error {
    color: #dc2626;
    font-size: 0.875rem;
    display: block;
    /* margin-top: 0.25rem; */
  }

  .note {
    font-size: 0.875rem;
    color: #666;
    margin-top: 0.5rem;
  }
</style>
