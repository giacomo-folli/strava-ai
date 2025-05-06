<script lang="ts">
  import { onMount } from "svelte";
  import { env } from "$env/dynamic/public";

  let status = "Processing...";
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
      return;
    }
    if (!email) {
      status = "Error: Missing email in storage";
      return;
    }

    try {
      const n8n_uri = env.PUBLIC_VITE_N8N_WEBHOOK_URL;

      const response = await fetch(n8n_uri, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ code, email }),
      });

      if (response.ok) {
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

<a href="/">Try again</a>

<h1>{status}</h1>
{#if isDev}
  <button on:click={sendCodeToN8n}>Resend</button>
{/if}
