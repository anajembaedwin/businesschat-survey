# BusinessChat Survey

Product validation survey for BusinessChat — a WhatsApp CRM tool for businesses.

## Live page

https://anajembaedwin.github.io/businesschat-survey

## What this is

A branching survey to validate product-market fit before launch.
Responses are collected via Google Sheets.

## Setup

1. Create a Google Apps Script web app (see below) and set a secret token in its script properties.
2. Deploy a Cloudflare Worker that receives the survey POST and forwards it to the Apps Script URL together with the secret token. Store the token as a Worker secret (`SECRET_TOKEN`), never in this repo.
3. Open `index.html` and set `SHEET_URL` to your Worker URL (the public endpoint, not the Apps Script URL).

> **Do not put the secret token in `index.html`.** Everything in that file is public once it is on GitHub Pages. The token must live only in the Worker and the Apps Script.

## Google Apps Script setup

1. Go to script.google.com
2. Create a new project
3. Add a script that validates the token, then appends the submitted fields as a row in your Sheet
4. Deploy as Web App: execute as Me, access to Anyone
5. Give the deployment URL and the token to the Worker as secrets

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
