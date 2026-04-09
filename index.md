---
layout: default
title: OpenClaw Draft Kit
---

# OpenClaw Draft Kit

**A desktop productivity tool for content creators to draft and publish short videos to TikTok through the official Content Posting API.**

OpenClaw Draft Kit is an open-source extension for the [OpenClaw](https://github.com/openclaw/openclaw) platform that helps individual creators move approved video drafts from their local workspace into their own TikTok drafts inbox, ready for final review and publishing inside the TikTok mobile app.

---

## What it does

| Step | What happens | Where |
|---|---|---|
| 1. **Authorize** | Creator signs in with their own TikTok account via official OAuth 2.0 | In a web browser on the creator's device |
| 2. **Select video** | Creator picks an approved video draft from their local workspace | Inside the OpenClaw desktop tool |
| 3. **Upload to drafts** | The tool calls TikTok's official Content Posting API to upload the video into the creator's **drafts inbox** | Direct HTTPS request to `open.tiktokapis.com` |
| 4. **Review in TikTok app** | Creator opens the TikTok mobile app, reviews the draft, and finalizes publishing | Inside the official TikTok mobile app |

**The final publish decision always happens inside the TikTok mobile app.** The tool itself never publishes content without the user's explicit in-app confirmation.

---

## Key principles

- 🔒 **Official API only** — uses exclusively the [TikTok Content Posting API](https://developers.tiktok.com/products/content-posting-api/). No scraping, no reverse-engineered clients, no third-party SDKs.
- 🔑 **OAuth 2.0** — creators authorize their own TikTok account. The tool never sees or stores TikTok passwords.
- 🏠 **Local-first** — access tokens are stored on the user's own device under `~/.openclaw/credentials/tiktok/` with permissions set to `0600`. Nothing is transmitted to any third party.
- 🤖 **AI-generated content labeled** — any content created with AI assistance is automatically tagged with `is_aigc=true` per TikTok policy requirements.
- 🚫 **No automation of violations** — no scheduling, no batch posting, no multi-account management, no growth-hacking features. Every upload is initiated by an explicit user action.
- 📝 **Audit log** — every publish action is recorded locally for compliance and troubleshooting.

---

## Features

- **Upload to Drafts** (inbox mode) — the recommended workflow: upload a video into the creator's drafts and let them finalize publishing in the TikTok app
- **Query Creator Info** — check allowed privacy levels and creator capabilities before any publish action
- **Publish Status** — poll the status of in-flight uploads
- **List Videos** — review the creator's own published videos (read-only)
- **Rate limit protection** — self-imposed daily publish cap to avoid `spam_risk` on the creator's account
- **Compliance helpers** — built-in validation for AI content labeling and commercial content disclosure

---

## Supported TikTok API products

This application integrates with the following TikTok for Developers products:

| Product | Scope | Purpose |
|---|---|---|
| **Login Kit** | `user.info.basic` | OAuth authorization and creator profile display |
| **Content Posting API** | `video.upload` | Upload video drafts to the creator's TikTok inbox |

All scope use is documented in [our App Review submission](https://developers.tiktok.com/).

---

## Installation

OpenClaw Draft Kit is distributed as an extension of the OpenClaw platform.

**Requirements**:

- OpenClaw desktop platform installed ([download](https://github.com/openclaw/openclaw))
- Node.js ≥ 22
- A TikTok developer account with Content Posting API enabled
- A verified domain for `PULL_FROM_URL` video sources (optional; only needed for carousel/remote-URL mode)

**Install**:

```bash
# 1. Enable the extension
openclaw plugin enable tiktok-publish

# 2. Configure your TikTok Developer App credentials
openclaw config set tiktok-publish.clientKey <your_client_key>
openclaw config set tiktok-publish.clientSecret <your_client_secret>
openclaw config set tiktok-publish.redirectUri https://<your-https-domain>/tiktok/oauth/callback

# 3. Authorize (follow the browser OAuth flow)
openclaw tiktok-publish login
```

**Source code**: [https://github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)

---

## Privacy & Data Handling Summary

- **What we receive from TikTok**: OAuth tokens (access_token, refresh_token, open_id) and optionally display_name + avatar_url if `user.info.basic` scope is granted
- **Where it's stored**: local device only, under `~/.openclaw/credentials/tiktok/` with permissions `0600`
- **What we send to TikTok**: only the video files and metadata you explicitly choose to upload, via TikTok's official API endpoints
- **What we do NOT collect**: passwords, real names, emails, phone numbers, followers lists, direct messages, or any information about other TikTok users
- **Third-party sharing**: **none**

For full details, see our **[Privacy Policy](./privacy/)**.

---

## Legal Documents

- 📄 **[Terms of Service](./terms/)** — your rights and responsibilities when using this application
- 🔒 **[Privacy Policy](./privacy/)** — complete details on how we handle your data

---

## Support

- **Source code / issue tracker**: [github.com/aixier/tiktok-publisher-legal](https://github.com/aixier/tiktok-publisher-legal)
- **OpenClaw platform**: [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)
- **TikTok for Developers**: [developers.tiktok.com](https://developers.tiktok.com/)
- **TikTok Community Guidelines**: [tiktok.com/community-guidelines](https://www.tiktok.com/community-guidelines)

For privacy or legal inquiries, please [open an issue](https://github.com/aixier/tiktok-publisher-legal/issues).

---

## Disclaimer

OpenClaw Draft Kit is an independent third-party application. It is **not affiliated with, endorsed by, sponsored by, or otherwise associated with TikTok Inc.** or ByteDance Ltd. "TikTok" is a trademark of its respective owner. All use of the TikTok name and APIs in this application is solely for the purpose of identifying the platform that users of this application voluntarily integrate with.

---

*Last updated: 2026-04-09*
