<script lang="ts">
    import { page } from "$app/state";
    import { onMount } from "svelte";
</script>

<svelte:head>
    <title>Strava Connection</title>
</svelte:head>

<main class="container">
    <slot />

    {#if !page?.route?.id?.includes("review")}
        <div class="logo">
            <img width="100px" src="/api_logo_cpt.png" alt="api-logo" />
        </div>
    {/if}
</main>

<style>
    .container {
        display: flex;
        position: relative;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 100vh;
        font-family: system-ui, sans-serif;
    }

    .logo {
        position: absolute;
        bottom: 25px;
        left: 20px;
    }

    :global(h1) {
        margin-bottom: 2rem;
        text-align: center;
        max-width: 600px;
        padding: 0 1rem;
    }
</style>
