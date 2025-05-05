<script lang="ts">
  import { onMount } from "svelte";

  let status = "Processing...";

  async function sendCodeToN8n() {
    const params = new URLSearchParams(window.location.search);
    const code = params.get("code");

    if (!code) {
      status = "Error: Missing authorization code";
      return;
    }

    try {
      const response = await fetch(import.meta.env.VITE_N8N_WEBHOOK_URL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ code }),
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

  onMount(() => {
    sendCodeToN8n();
  });
</script>

<h1>{status}</h1>
