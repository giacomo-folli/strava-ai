# Strava OAuth Connection

A SvelteKit application that handles Strava OAuth2 authentication and forwards the authorization code to an n8n webhook.

## Setup

1. Copy `.env.example` to `.env`
2. Update the environment variables in `.env`:
   - `VITE_STRAVA_CLIENT_ID`: Your Strava API client ID
   - `VITE_REDIRECT_URI`: Your callback URL (e.g., https://your-domain.com/callback)
   - `VITE_N8N_WEBHOOK_URL`: Your n8n webhook URL

## Development

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
```

## Deploy

This application can be deployed to any static hosting service that supports SvelteKit applications (Netlify, Vercel, etc.).

Make sure to configure the environment variables in your hosting provider's dashboard.
