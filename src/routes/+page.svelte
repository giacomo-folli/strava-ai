<script lang="ts">
  const clientId = import.meta.env.VITE_STRAVA_CLIENT_ID;
  const redirectUri = encodeURIComponent(
    import.meta.env.VITE_REDIRECT_URI || ""
  );
  const scopes = "read,activity:read";

  function connectStrava() {
    const authUrl = `https://www.strava.com/oauth/authorize?client_id=${clientId}&response_type=code&redirect_uri=${redirectUri}&approval_prompt=auto&scope=${scopes}`;
    window.location.href = authUrl;
  }
</script>

<h1>Connect Your Strava Account</h1>
<button on:click={connectStrava}>Connect with Strava</button>
