# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Project

This is a pure static HTML project — no build step, no package manager. Open any file directly in a browser:

```bash
# Quick local server (Python)
python -m http.server 8080

# Or with Node
npx serve .
```

Then open `http://localhost:8080/login.html` as the entry point.

## Architecture

The project has two distinct purposes coexisting in the same repo:

### 1. Crypto Market Circle — Auth + Dashboard (`login.html`)
A single-page auth flow backed by **AWS Cognito** (no backend server). The entire app lives in one file:
- Dynamically loads `amazon-cognito-identity-js@6.3.12` from CDN (with three fallback CDNs)
- Hardcoded Cognito pool: `us-east-1_w8Xdhhx6F` / client `7773bppmtcpi51f68jce6n04m` (us-east-1)
- Auth states managed by toggling `display:none` on form elements: sign-in → sign-up → email verification → forgot password → reset password
- After login, hides `#login-container` and shows `#home-container` dashboard; `exam1()` navigates to `Test1.html`

### 2. AWS SAA-C03 Exam Prep (`index.html`, `Test1–4.html`, `Email.html`)
- `index.html` is a navigation hub linking to the test pages and `Email.html`
- `Test1–4.html` are standalone question tables with inline CSS and data; each uses domain-color-coded tags (Resilient=red, Performance=blue, Secure=purple, Cost=orange) and category left-border colors (storage, database, security, compute, etc.)
- All filtering/search is done client-side with vanilla JavaScript

### Shared Design System
All pages share the same inline CSS design language: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)` purple gradient background, white card containers, `Segoe UI` font stack. There is no shared CSS file — styles are duplicated per page.
