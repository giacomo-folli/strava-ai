<script lang="ts">
  import { onMount } from "svelte";
  import { env } from "$env/dynamic/public";
  import { goto } from "$app/navigation";

  let status = "Processing...";
  let success = false;
  let isDev = env.PUBLIC_NODE_ENV == "dev";

  function getEmailFromLocal() {
    const email = sessionStorage.getItem("user-email");
    sessionStorage.clear();
    return email;
  }

  async function sendCodeToN8n() {
    const params = new URLSearchParams(window.location.search);
    const code = params.get("code");

    const email = getEmailFromLocal();

    if (!code) {
      status = "Error: Missing authorization code";
      await goto("/");
    }

    if (!email) {
      status = "Error: Missing email in storage";
      await goto("/");
    }

    try {
      const n8n_uri = env.PUBLIC_VITE_N8N_WEBHOOK_URL;

      const response = await fetch(n8n_uri, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ code, email }),
      });

      if (response.ok) {
        success = true;
        status = "✅ Strava connected successfully!";
      } else {
        status = "❌ Connection failed. Please try again.";
      }
    } catch (error) {
      status = "❌ Network error. Please try again.";
    }
  }

  onMount(() => sendCodeToN8n());
</script>

{#if !success}
  <a href="/">Try again</a>
{/if}

<h1>{status}</h1>
<p>
  Soon you'll start receiving custom training session analysis powered by your
  AI coach. Stay tuned for personalized insights to help you improve your
  performance!
</p>

{#if isDev}
  <button on:click={sendCodeToN8n}>Resend</button>
{/if}

<style>
  button {
    padding: 0.75rem 1.5rem;
    font-size: 1.2rem;
    background-color: #fc4c02;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  button:hover {
    background-color: #e34402;
  }
</style>
