<script lang="ts">
    import { onMount } from "svelte";

    let email = "";
    let walkthroughDialog: HTMLDialogElement;
    let currentStep = 0;

    const walkthroughSteps = [
        {
            title: "Connect a Strava account",
            description:
                "Runners entered an email address and approved Strava OAuth access to the activity data the coach needed.",
        },
        {
            title: "Hand off the authorization to n8n",
            description:
                "After Strava returned an authorization code, the SvelteKit callback sent it with the email address to an n8n webhook to start the follow-up workflow.",
        },
        {
            title: "Turn workout data into coaching",
            description:
                "The workflow used AI to turn signals such as pace, heart rate, and cadence into a performance summary and goal-aware training recommendations.",
        },
        {
            title: "Deliver useful next steps",
            description:
                "Runners received activity analysis, goal progress, training options, and practical tips by email.",
        },
    ];

    function connectStrava() {
        currentStep = 0;
        walkthroughDialog.showModal();
    }

    function showNextStep() {
        if (currentStep === walkthroughSteps.length - 1) {
            walkthroughDialog.close();
            return;
        }

        currentStep += 1;
    }

    function showPreviousStep() {
        currentStep = Math.max(0, currentStep - 1);
    }

    function handleWalkthroughCancel() {
        walkthroughDialog.close();
    }

    function handleWalkthroughKeydown(event: KeyboardEvent) {
        if (event.key === "Escape" && walkthroughDialog.open) {
            event.preventDefault();
            walkthroughDialog.close();
        }
    }

    onMount(() => walkthroughDialog.showModal());
</script>

<svelte:window on:keydown={handleWalkthroughKeydown} />

<h1>Connect Your Strava Account</h1>

<div class="form-group">
    <label for="email">Email for Activity Updates</label>
    <input
        type="email"
        id="email"
        bind:value={email}
        placeholder="Enter your email"
    />
    <p class="note">
        We'll send your activity analysis and coaching tips to this email
        address.
    </p>
</div>

<!-- Connect with Strava -->
<button class="connect" on:click={connectStrava}>
    <img
        width="250px"
        height="auto"
        src="/btn_strava_connect.svg"
        alt="connect"
        class="connect-img"
    />
</button>

<style>
    .connect-img:hover {
        cursor: pointer;
        scale: 1.01;
    }

    .connect {
        background-color: transparent;
        color: transparent;
        box-shadow: none;
        border: none;
    }

    .form-group {
        margin-bottom: 2rem;
        width: 100%;
        max-width: 400px;
    }

    .support-button {
        position: fixed;
        bottom: 20px;
        right: 20px;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-color: #fc4c02;
        color: white;
        border: none;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        transition: transform 0.2s ease-in-out;
        z-index: 1000;
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

    .note {
        font-size: 0.875rem;
        color: #666;
        margin-top: 0.5rem;
    }

    .walkthrough-dialog {
        width: min(560px, calc(100vw - 32px));
        max-height: calc(100vh - 32px);
        margin: auto;
        padding: 0;
        border: 0;
        border-radius: 8px;
        color: #111;
        box-shadow: 0 16px 48px rgba(0, 0, 0, 0.24);
    }

    .walkthrough-dialog::backdrop {
        background: rgba(0, 0, 0, 0.56);
    }

    .walkthrough {
        padding: clamp(1.5rem, 5vw, 2.5rem);
    }

    .walkthrough-close {
        display: block;
        width: 2rem;
        height: 2rem;
        margin: 0 0 1rem auto;
        border: 0;
        border-radius: 50%;
        background: transparent;
        color: #333;
        font-size: 1.5rem;
        line-height: 1;
        cursor: pointer;
    }

    .walkthrough-close:hover {
        background: #f2f2f2;
    }

    .walkthrough-dialog :focus-visible {
        outline: 3px solid #fc4c02;
        outline-offset: 3px;
    }

    .walkthrough h2 {
        margin: 0 0 0.75rem;
        font-size: clamp(1.4rem, 5vw, 1.8rem);
        line-height: 1.2;
    }

    .walkthrough-description {
        color: #555;
        line-height: 1.55;
    }

    .walkthrough-progress {
        height: 4px;
        margin: 1.75rem 0 0.75rem;
        overflow: hidden;
        border-radius: 4px;
        background: #e8e8e8;
    }

    .walkthrough-progress span {
        display: block;
        height: 100%;
        background: #fc4c02;
    }

    .walkthrough-step-count {
        margin-bottom: 1.25rem;
        color: #555;
        font-size: 0.875rem;
    }

    .walkthrough-step h3 {
        margin-bottom: 0.5rem;
        font-size: 1.2rem;
    }

    .walkthrough-step p {
        color: #444;
        line-height: 1.6;
    }

    .walkthrough-actions {
        display: flex;
        justify-content: space-between;
        gap: 1rem;
        margin-top: 2rem;
    }

    .walkthrough-actions button {
        min-height: 44px;
        padding: 0.65rem 1rem;
        border: 1px solid #fc4c02;
        border-radius: 4px;
        background: #fc4c02;
        color: white;
        font: inherit;
        cursor: pointer;
    }

    .walkthrough-actions button:hover:not(:disabled) {
        background: #e34402;
    }

    .walkthrough-actions button:disabled {
        border-color: #ccc;
        background: #f2f2f2;
        color: #666;
        cursor: not-allowed;
    }


    .support-button {
        position: fixed;
        bottom: 20px;
        right: 20px;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        background-color: #fc4c02;
        color: white;
        border: none;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        transition: transform 0.2s ease-in-out;
    }

    .support-button:hover {
        transform: scale(1.1);
    }

    .support-button svg {
        width: 24px;
        height: 24px;
    }

    .support-button:active {
        transform: scale(0.95);
    }

</style>

<!-- Support Button -->
<button class="support-button" on:click={() => window.open('https://github.com/giacomo-folli/strava-ai/issues', '_blank')}>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white">
        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm0 14.2c-2.5 0-4.71-1.28-6-3.22.03-1.99 4-3.08 6-3.08 1.99 0 5.97 1.09 6 3.08-1.29 1.94-3.5 3.22-6 3.22z"/>
    </svg>
</button>

<dialog
    class="walkthrough-dialog"
    bind:this={walkthroughDialog}
    aria-labelledby="walkthrough-title"
    aria-describedby="walkthrough-description"
    on:cancel={handleWalkthroughCancel}
>
    <div class="walkthrough">
        <button
            type="button"
            class="walkthrough-close"
            aria-label="Close walkthrough"
            on:click={() => walkthroughDialog.close()}
        >
            <span aria-hidden="true">&times;</span>
        </button>

        <h2 id="walkthrough-title">
            Unfortunately, this app is not active anymore.
        </h2>
        <p id="walkthrough-description" class="walkthrough-description">
            The live Strava connection is unavailable, but you can still explore
            how this project worked.
        </p>

        <div
            class="walkthrough-progress"
            role="progressbar"
            aria-label="Walkthrough progress"
            aria-valuemin="1"
            aria-valuemax={walkthroughSteps.length}
            aria-valuenow={currentStep + 1}
        >
            <span
                style={`width: ${((currentStep + 1) / walkthroughSteps.length) * 100}%`}
            ></span>
        </div>
        <p class="walkthrough-step-count">
            Step {currentStep + 1} of {walkthroughSteps.length}
        </p>

        <section class="walkthrough-step" aria-live="polite" aria-atomic="true">
            <h3>{walkthroughSteps[currentStep].title}</h3>
            <p>{walkthroughSteps[currentStep].description}</p>
        </section>

        <div class="walkthrough-actions">
            <button
                type="button"
                on:click={showPreviousStep}
                disabled={currentStep === 0}
            >
                Back
            </button>
            <button type="button" on:click={showNextStep}>
                {currentStep === walkthroughSteps.length - 1
                    ? "Finish"
                    : "Next"}
            </button>
        </div>
    </div>
</dialog>
