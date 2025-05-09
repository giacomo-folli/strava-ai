<script lang="ts">
    import { page } from "$app/state";
</script>

<svelte:head>
    <title>Strava Connection</title>
</svelte:head>

<main class="container">
    <slot />

    {#if !page?.route?.id?.includes("review") && !page?.route?.id?.includes("confirmation")}
        <div class="logo">
            <img width="100px" src="/api_logo_cpt.png" alt="api-logo" />
        </div>
    {/if}
</main>

<style>
    :global(*) {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    :global(html, body) {
        height: 100%;
        overflow: hidden;
    }

    .container {
        display: flex;
        position: relative;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        font-family: system-ui, sans-serif;
        padding: 20px;
        box-sizing: border-box;
    }

    .logo {
        position: absolute;
        bottom: 20px;
        left: 25px;
    }

    :global(h1) {
        margin-bottom: 2rem;
        text-align: center;
        max-width: 600px;
        padding: 0 1rem;
    }
</style>
