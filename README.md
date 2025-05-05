# 🛠 Guide: Build a Frontend for Strava OAuth Connection

## 🎯 Objective

Create a simple web frontend that:

- Allows users to **connect their Strava account** via OAuth2.
- Redirects users to a **Strava OAuth page**.
- Handles the **OAuth callback** by forwarding the `code` to an `n8n` webhook.
- Provides **basic user feedback** after connecting.
- (Optional) Can be hosted as a single static page (e.g., via Netlify, Vercel, GitHub Pages).

---

## 📋 Requirements

- **Single-page UI** (HTML + JS)
- **"Connect with Strava"** button
- Dynamic redirection to the Strava OAuth URL
- Handling of the OAuth **callback** from Strava (`code`)
- Forwarding the `code` to your `n8n` webhook for token exchange
- Displaying a **success or failure message** to the user

---

## 🔐 Strava OAuth Info (You provide to bolt.new)

- `STRAVA_CLIENT_ID`: from Strava API settings
- `REDIRECT_URI`: something like `https://yourdomain.com/callback.html`
- `SCOPES`: `read,activity:read`
- `n8n_WEBHOOK_CALLBACK_URL`: something like `https://n8n.yourdomain.com/webhook/strava-callback`

---

## ✅ Step-by-Step Tasks for bolt.new

---

### 1. **Landing Page (index.html)**

**Purpose**: Contains a button that sends the user to the Strava OAuth page.

---

### 2. **Callback Page (callback.html)**

**Purpose**: Handles the OAuth `code`, then sends it to your `n8n` webhook.

---

## 🧠 Notes for bolt.new

- Use environment variables or configuration flags for `STRAVA_CLIENT_ID`, `REDIRECT_URI`, and `n8n` endpoint.
- This frontend is static and deployable on Netlify, Vercel, or any CDN.
- All logic happens client-side — the token exchange is handled server-side by **n8n**, keeping credentials secure.

---

## 📦 Deliverables

- `index.html`: Main connection page
- `callback.html`: OAuth2 code handler and forwarder
- `style.css` (optional): Basic styling
- `README.md`: Instructions for deploying and configuring environment values

---
