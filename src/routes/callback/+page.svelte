<script lang="ts">
  import { onMount } from "svelte";
  import { env } from "$env/dynamic/public";

  let status = "Processing...";

  async function sendCodeToN8n() {
    const params = new URLSearchParams(window.location.search);
    const code = params.get("code");
    const email = params.get("email");

    if (!code) {
      status = "Error: Missing authorization code";
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

<a href="/">Go Back</a>

<h1>{status}</h1>
<button on:click={sendCodeToN8n}>Resend</button>
