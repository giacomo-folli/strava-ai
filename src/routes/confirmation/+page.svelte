<script lang="ts">
    import { onMount } from "svelte";

    let emailContent: string;
    let previewName = "John";

    onMount(async () => {
        const response = await fetch("/confirmation-template.html");
        emailContent = await response.text();

        // Replace placeholder with preview name
        emailContent = emailContent.replace("{{NAME}}", previewName);
    });
</script>

{#if emailContent}
    {@html emailContent}
{:else}
    <div class="loading">Loading template...</div>
{/if}

<style>
    .loading {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        font-size: 1.2rem;
        color: #666;
    }

    :global(body) {
        margin: 0;
        padding: 0;
    }
</style>
