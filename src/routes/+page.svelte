<script lang="ts">
    import { env } from "$env/dynamic/public";

    const scopes = "activity:read_all,read_all";

    let email = "";
    let emailError = "";

    function validateEmail(email: string) {
        const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return re.test(email);
    }

    function storeEmailLocal(email: string) {
        sessionStorage.setItem("user-email", email);
    }

    function connectStrava() {
        if (!email || !validateEmail(email)) {
            emailError = "Please enter a valid email address";
            return;
        }

        storeEmailLocal(email);

        const clientId = env.PUBLIC_VITE_STRAVA_CLIENT_ID;
        const redirectUri = `${window.location.origin}/callback`;

        const queryParams = new URLSearchParams({
            client_id: clientId,
            response_type: "code",
            approval_prompt: "auto",
            redirect_uri: redirectUri,
            scope: scopes,
        });

        const authUrl = `https://www.strava.com/oauth/authorize?${queryParams.toString()}`;

        window.location.href = authUrl;
    }
</script>

<h1>Connect Your Strava Account</h1>

<div class="form-group">
    <label for="email">Email for Activity Updates</label>
    <input
        type="email"
        id="email"
        bind:value={email}
        placeholder="Enter your email"
        on:input={() => (emailError = "")}
    />
    {#if emailError}
        <span class="error">{emailError}</span>
    {/if}
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

    .error {
        color: #dc2626;
        font-size: 0.875rem;
        display: block;
        /* margin-top: 0.25rem; */
    }

    .note {
        font-size: 0.875rem;
        color: #666;
        margin-top: 0.5rem;
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
