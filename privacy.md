---
layout: default
title: Privacy Policy — OpenClaw Draft Kit
---

# Privacy Policy

**Effective date: 2026-04-09**  
**Last updated: 2026-04-09**

This Privacy Policy describes how the OpenClaw Draft Kit application ("the Application", "we", "us", or "our") handles information received from TikTok and from you ("the User", "you"). We are committed to protecting your privacy and being transparent about what data we access and how we use it.

**Summary (plain English)**: We run entirely on your own device. We receive OAuth tokens and basic profile information from TikTok when you authorize the Application, and we use them solely to upload videos you choose into your own TikTok drafts. We do not transmit your data to any third party, we do not use cloud storage, and we do not share anything with anyone.

## 1. Information We Receive

When you authorize the Application with your TikTok account via OAuth 2.0, TikTok provides us with the following information:

### 1.1 Authentication Tokens

- **`access_token`** — a bearer token used to make API calls on your behalf. Valid for 24 hours.
- **`refresh_token`** — a token used to obtain a new access token when the current one expires. Valid for up to 365 days.
- **`expires_in`** — the number of seconds until the access token expires.
- **`open_id`** — a stable, opaque identifier issued by TikTok that identifies your TikTok account within the context of this specific Application. It is not your username and is not usable outside this Application.
- **`scope`** — the list of permissions you granted.

### 1.2 Profile Information (only if you grant `user.info.basic`)

- Your TikTok **display name**
- Your TikTok **avatar URL**
- Your TikTok **open_id**

This profile information is displayed to you within the Application so that you can confirm which TikTok account is currently connected. It is not transmitted anywhere else.

### 1.3 Video Upload Data

When you explicitly choose to upload a video, the Application reads the video file from your local file system (or a URL you provide) and streams it to TikTok's official upload endpoint. The Application does not retain a copy of the video file beyond the duration of the upload.

## 2. Information We Do NOT Collect

The Application does **not** collect, receive, or process:

- ❌ Your TikTok **password** — OAuth 2.0 means we never see it
- ❌ Your **email address** or **phone number**
- ❌ Your **real name** or any personal identifying information other than the profile information listed above
- ❌ Your **TikTok followers, following list, or direct messages**
- ❌ Information about **other TikTok users** (including users who interact with your content)
- ❌ Your **browsing history**, **device identifiers**, **advertising IDs**, or **location data**
- ❌ Any information from **users under 18**

## 3. How We Use the Information

We use the information we receive from TikTok exclusively for the following purposes:

1. **OAuth tokens** are used to authenticate API calls to TikTok's Content Posting API on your behalf, for operations you explicitly initiate within the Application.
2. **`open_id`** is used to associate stored tokens with the correct user session when the Application is used by more than one TikTok account on the same device.
3. **Profile information** (display_name, avatar_url) is used to show you which TikTok account is currently connected, so you can confirm the intended target before publishing.
4. **Video files** are streamed directly from your device (or the URL you provide) to TikTok's official upload endpoint. The Application does not store, analyze, or inspect video content.

We do **not** use your information for:

- ❌ Advertising or marketing
- ❌ Analytics or behavioral tracking
- ❌ Training machine-learning models
- ❌ Profiling or automated decision-making
- ❌ Any purpose not explicitly listed above

## 4. Data Storage and Security

### 4.1 Where your data lives

All authentication tokens and local state are stored **on your own device** in the following locations:

- **OAuth tokens**: `~/.openclaw/credentials/tiktok/<open_id>.json` — file permissions restricted to the owner (chmod 0600 on Unix-like systems)
- **Rate-limit state**: `~/.openclaw/credentials/tiktok/rate-<open_id>.json` — file permissions restricted to the owner
- **Audit log**: `~/.openclaw/logs/tiktok-publish.jsonl` — records the timestamp, action, and outcome of each publish operation for your own compliance and troubleshooting purposes

The Application **does not** use any cloud database, remote key-value store, or third-party server for storing your data. There is no "backend" that holds your tokens.

### 4.2 Security measures

- Token files are created with restrictive file permissions (`0600`), meaning only the operating system user who installed the Application can read them.
- Token files are never transmitted over the network, except as needed to call TikTok's official API endpoints (`open.tiktokapis.com`, `www.tiktok.com`).
- The Application uses HTTPS for all TikTok API communication.
- No telemetry, crash reports, or usage analytics are sent anywhere.

### 4.3 Your responsibility

You are responsible for the security of the device on which the Application is installed. If your device is compromised, anyone with access to your user account on that device could read the stored tokens. We recommend:

- Using full-disk encryption
- Not running the Application on shared or untrusted devices
- Revoking the Application's access from your TikTok account if you suspect your device has been compromised

## 5. Data Sharing

**We do not share, sell, rent, lease, transfer, or otherwise disclose your information to any third party under any circumstances.**

The only network destinations your data is transmitted to are TikTok's own official servers, and only for the purpose of fulfilling API requests you explicitly initiate:

- `https://open.tiktokapis.com/v2/oauth/token/` — token exchange and refresh
- `https://open.tiktokapis.com/v2/user/info/` — profile fetch
- `https://open.tiktokapis.com/v2/post/publish/...` — upload and status queries
- `https://open.tiktokapis.com/v2/video/list/` — list your own videos (only if `video.list` scope is granted)
- TikTok upload endpoints returned dynamically by the above API calls

No other network destinations are contacted as part of the Application's core functionality.

## 6. Data Retention

Tokens are retained on your local device until one of the following occurs:

- You delete the token file manually
- The refresh_token expires (up to 365 days after issuance) and cannot be refreshed
- You uninstall the Application
- You revoke the Application's authorization from your TikTok account settings

You can delete all locally stored data at any time by running:

```
rm -rf ~/.openclaw/credentials/tiktok/
rm -f ~/.openclaw/logs/tiktok-publish.jsonl
```

## 7. Your Rights and Choices

You have the following rights regarding your data:

- **Access**: All data stored by the Application is in local JSON/JSONL files under `~/.openclaw/` that you can read directly.
- **Deletion**: You can delete all Application data at any time using the `rm` commands above.
- **Revocation**: You can revoke the Application's OAuth access at any time from your TikTok account: **Settings → Privacy → Apps and sessions → Manage app permissions**. Revoking access does **not** delete your local token files; you should also delete them manually if you wish to fully disconnect.
- **Export**: Your tokens and audit log are plain JSON/JSONL files that you can copy, back up, or share at your discretion.

## 8. Children's Privacy

The Application is **not intended for users under the age of 18**. We do not knowingly receive or process any information from users under 18. If you are under 18, please do not use the Application. If you believe that a user under 18 has used the Application, please contact us using the information in Section 12 and we will take appropriate steps.

## 9. International Users

The Application is designed to run entirely on your own device. We do not have any servers or data processing facilities. Your data stays where your device is. Your interaction with TikTok's servers is governed by TikTok's own [Privacy Policy](https://www.tiktok.com/legal/privacy-policy), which you should review separately.

## 10. TikTok's Data Handling

Any information you send to TikTok via the Application (including videos you upload and API calls you make) is subsequently handled by TikTok under [TikTok's Privacy Policy](https://www.tiktok.com/legal/privacy-policy). We have no control over, and assume no responsibility for, the privacy practices of TikTok or any other third party.

## 11. Changes to This Privacy Policy

We may update this Privacy Policy from time to time to reflect changes in our practices, legal requirements, or TikTok's developer policies. When we do, we will update the "Last updated" date at the top of this page. Material changes will be highlighted in the commit history of this repository. Your continued use of the Application after such changes constitutes your acceptance of the updated Privacy Policy.

## 12. Contact

For privacy-related questions, concerns, or requests, please open an issue on the [GitHub repository](https://github.com/aixier/tiktok-publisher-legal/issues).

You can also revoke the Application's access directly from your TikTok account at any time, without contacting us.

---

[Back to home](./) • [Terms of Service](./terms)
