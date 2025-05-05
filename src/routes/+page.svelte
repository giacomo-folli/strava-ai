<script lang="ts">
  import { env } from "$env/dynamic/public";

  const clientId = env.PUBLIC_VITE_STRAVA_CLIENT_ID;
  const redirectUri = window.location.href + "/callback";

  const scopes = "read,activity:read";

  function connectStrava() {
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
<button on:click={connectStrava}>Connect with Strava</button>
