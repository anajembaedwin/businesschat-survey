# BusinessChat Survey

Product validation survey for BusinessChat — a WhatsApp CRM tool for businesses.

## Live page

https://anajembaedwin.github.io/businesschat-survey

## What this is

A branching survey to validate product-market fit before launch.
Responses are collected via Google Sheets.

## Setup

1. Create a Google Apps Script web app (see below)
2. Open `index.html` and replace:
   - `YOUR_APPS_SCRIPT_URL_HERE` with your Apps Script deployment URL
   - `YOUR_SECRET_TOKEN_HERE` with a secret string of your choice (e.g. `bzy-2025-xk91`)
3. Use the same token in the Apps Script code

## Google Apps Script setup

1. Go to script.google.com
2. Create a new project
3. Paste the Apps Script code from the `/docs` folder
4. Deploy as Web App — execute as Me, access to Anyone
5. Copy the deployment URL into `index.html`

## How everything connects
```
Browser (GitHub Pages)
    ↓  POST /submit  (no secrets)
Cloudflare Worker
    ↓  POST + SECRET_TOKEN  (server-side only)
Google Apps Script
    ↓  validates token, writes row
Google Sheets
```
## Survey flow

- Splash page → Role selection (branches by role) → WhatsApp usage →
  Pain points → Pain score → Pricing → Open feedback → Email → Result

## Tech

Plain HTML/CSS/JS — no frameworks, no build step.
Hosted on GitHub Pages.
