---
title: RoValra API Privacy Policy
tags:
    - Backend
    - Legal
    - GDPR
---

**Privacy Policy for RoValra Chrome Extension**

**Effective Date:** September 22, 2026

**Introduction**

This Privacy Policy describes how the RoValra Chrome extension ("the Extension") handles user data. We are committed to protecting your privacy and ensuring transparency about our data practices.

<!-- section:data-controller:fas fa-building -->
## Data Controller

RoValra is responsible for the personal data it processes in connection with the Extension and its related services. For privacy questions, requests, or complaints, contact **RoValraContact@gmail.com**. 

<!-- section:information-collection:fas fa-info-circle -->
## Information Collection

To provide a consistent experience across different devices and to enable account-specific features, RoValra collects limited data for all users:

- **No Unnecessary Tracking:** RoValra does **not** track your browsing history on Roblox or any other websites, nor does it log the specific games you visit.

- **Roblox page and API data:** To provide its Roblox features, the Extension may process public Roblox profile information, PlaceIds, serverIds, and information required to identify or interact with Roblox game servers. This processing is limited to the Extension's features. RoValra does **not** collect cookies, Roblox private messages, chat messages, or general browsing history through these features.

- **General Users (Non-Donators):**
    - **Authentication:** To enable account-linked features (like status bubbles or environments), the Extension may initiate an OAuth session automatically in the background. This process is used to verify account ownership and provide secure access to server-side features without requiring manual login.
    - **Stored Data:** We store your **Roblox User ID** and **Username**. This data is necessary to associate your configuration and settings with your account across devices.
- **User-Set Information:** We store information you explicitly configure within the extension (such as status text, badges, or specific settings) to ensure your preferences persist.
    - **Visibility:** Some user-set information, such as a status, may be made visible to other RoValra users who use the Extension.

- **Donators (OAuth and Badge Features):**
    - Data collection occurs **only** after explicit OAuth authentication.
    - **What is stored:**
        - **Roblox User ID:** Used to uniquely identify your account.
        - **Roblox Username:** To display your identity within the extension.
        - **Donation Amount:** To track your contribution tier.
        - **Donator Badge Status:** To remember your toggle preferences.
        - **OAuth Tokens:** Cryptographic keys required to maintain your session.
        - **User-Set Information:** This includes custom status text, environment choices, and other personalized settings configured within the RoValra extension.

<!-- section:oauth-authentication:fas fa-lock -->
## OAuth & Verification Systems

To manage account-linked features, RoValra uses a background authentication system. 

**Terminology:** Within this policy and the extension, the term **"OAuth"** refers collectively to both the **Official Roblox OAuth system** and our **Fallback Authentication method**.

- **Background Processing:** Authentication is performed automatically in the background to ensure features remain active without interrupting your browsing.
- **Token Storage:** For official OAuth, we store an **Access Token** (identity verification) and a **Refresh Token** (session maintenance).
- **Feature Usage:** All users (donators and non-donators) using specific server-side features utilize the same OAuth authentication system to maintain secure sessions and feature access.
- **Strict Limitations:**
    - **Read-Only Scope:** Tokens allow us to read public profile data only. They **cannot** spend Robux, change passwords, or trade items.
    - **Low Risk Permissions:**

| Permission            | Description                                                      | Risk Level |
| :-------------------- | :--------------------------------------------------------------- | :--------- |
| **Read User ID**      | View your Roblox User ID to know who you are.                    | **Low**    |
| **Read User Profile** | View your username, display name, user avatar, and profile link. | **Low**    |

<!-- section:fallback-auth:fas fa-sign-in-alt -->
## Fallback Authentication

In the event that the official Roblox OAuth system is unavailable or fails to function, RoValra provides a Fallback Authentication method:

- **Verification Method:** This process involves you favoriting a specific, designated Roblox experience for a few seconds and then unfavoriting it.
- **Purpose:** This action allows our servers to verify your ownership of the account by checking public activity logs.
- **Security:** This method does not require any passwords or sensitive tokens and is used solely to verify account identity when standard OAuth is offline.

<!-- section:local-storage:fas fa-hdd -->
## Local Storage

RoValra uses your browser's local storage to remember your preferences and support extension features.

- **Configuration:** Your extension settings (toggles, UI choices) are stored locally.
- **Caching:** We may cache public Roblox data (like friend lists or group info) locally to reduce network requests and improve load times.

<!-- section:extension-specific-data:fas fa-puzzle-piece -->
## Extension-Specific Data Practices

The Extension may handle the following data for specific features:

- **Location coordinates:** If a feature uses your location, RoValra may store your latitude and longitude in the Extension's local storage on your device. These coordinates are stored locally only and are not sent to RoValra servers or third parties by the Extension's location feature.
- **Local Roblox API key:** RoValra may generate a Roblox API key for local use on your device. The key is created with **no permissions** and cannot perform actions on your Roblox account. It is used only to support Roblox APIs that require a key, is stored locally, and is not transmitted to RoValra servers or third parties.
- **Optional Discord connection:** If you choose to connect your Discord account to RoValra to receive donator roles in RoValra's official Discord server, we may store your Discord user ID. We use it only to associate your Discord account with your RoValra donator status and assign or manage the applicable server role. Connecting Discord is optional; you can request removal of this association using the contact information below.
- **Playtime tracking:** When playtime tracking is enabled, RoValra collects and stores information about your Roblox playtime on RoValra's servers so playtime features can display your playtime within RoValra. Playtime tracking can be disabled at any time; when disabled, RoValra stops collecting and storing playtime data for these features.

We do **not** store your Discord username, Discord OAuth tokens, or Discord server-membership data.

The Extension does not collect any of this information unless the relevant feature is used or, in the case of Discord, you choose to connect your account.

<!-- section:limited-use:fas fa-scale-balanced -->
## Limited Use of User Data

RoValra's use of user data is limited to providing and improving the Extension's user-facing features, maintaining account-linked settings and donator benefits, preventing abuse, and protecting the security and integrity of RoValra. We do not sell user data or use it for personalized, retargeted, or interest-based advertising. We do not transfer user data to third parties except when necessary to provide a requested feature, comply with legal obligations, protect security, or complete a permitted change in control of the service. We do not permit humans to review user data except with the user's consent for support, when necessary for security, or when required by law.

<!-- section:extension-permissions:fas fa-shield-halved -->
## Extension Permissions

The Extension requests the following permissions to provide its features:

- **`declarativeNetRequest`:** Used to modify the user agent on requests made by the Extension where required for compatibility with Roblox systems. The Extension does not use this permission to monitor your general browsing activity.
- **`storage`:** Used to save Extension settings, cached data, location coordinates, and the local Roblox API key in the browser's Extension storage.
- **`scripting`:** Used to inject the Extension's feature scripts into Roblox pages.

The Extension's host access is limited to Roblox domains and Roblox APIs listed in its manifest. Its content scripts run on Roblox pages to provide the Extension's features. Optional permissions, including `webNavigation`, `contextMenus`, and `webRequest`, are requested only when a feature requires them.

The permissions and data practices described here are intended to match the Extension's Chrome Web Store listing and manifest. If a future version introduces a new permission or a materially different data practice, we will update this policy and the relevant store disclosures before or when that feature is introduced.

<!-- section:no-tracking:fas fa-eye-slash -->
## No Tracking or Analytics

We believe in absolute privacy. RoValra does **not** use any analytics suites (like Google Analytics). We do not track your browsing history, your search history on external search engines, or your personal real-world identity. **Crucially, we do not track or log which games you visit on Roblox or any of your on-site activity.**

<!-- section:optional-data-sharing:fas fa-share-alt -->
## Optional Data Sharing

For certain features, the Extension may send specific non-personal data:

- **Data points:** Transmits only **PlaceIds** and **serverIds**.
- **Purpose:** Used to enhance server-tracking and uptime features.
- **Control:** Completely optional; can be disabled in settings at any time.
- **Privacy:** No data that could link a user to this info is explicitly logged.


<!-- section:user-rights:fas fa-user-shield -->
## User Rights: Access, Control, and Erasure

We respect your control over your personal data. Depending on your location and the applicable law, you may have rights to access, correct, restrict, object to, or request deletion of your personal data. You may also have the right to receive a portable copy of certain data.

- **Right to Access:** You may request a copy of the data we hold (ID, Username, Tier).
- **Right to Erase:** You may request permanent deletion of your data.
    - *Note: This revokes tokens and removes access to Donator Badges.*
- **Discord Association:** You may request removal of the Discord user ID associated with your RoValra donator status. This may remove or prevent synchronization of the applicable Discord role.
- **Local Data:** Local settings, cached data, location coordinates, and the local Roblox API key can be removed through your browser's extension-data controls or by uninstalling the Extension. Server-side data is not removed automatically by uninstalling.
- **Contact:** Email **RoValraContact@gmail.com** with subject "Right to Access" or "Right to Erase".

You may withdraw optional consent at any time by disconnecting Discord, disabling the relevant Extension feature, clearing the Extension's local data, or contacting us. Withdrawal does not affect processing that occurred before withdrawal or processing required for security or legal obligations. If you believe we have not handled your data appropriately, you may also complain to the data-protection or privacy regulator in your country.

<!-- section:lawful-basis:fas fa-gavel -->
## Legal Bases for Processing

Where data-protection law requires a legal basis, RoValra processes data as follows:

- **Requested features and account services:** Processing is necessary to provide features you request, such as account-linked settings, authentication, donator benefits, and Discord role synchronization.
- **Optional features:** Processing is based on your choice when you enable a feature such as location-related functionality or connect Discord.
- **Security and abuse prevention:** Processing may be based on our legitimate interest in securing, maintaining, and preventing abuse of the Extension and its services, subject to applicable law.
- **Legal obligations:** We may process or retain data when necessary to comply with law or respond to lawful requests.

<!-- section:data-security:fas fa-shield-alt -->
## Data Security

We use industry-standard security to protect our users:

- **Local Processing:** Local settings, cached data, location coordinates, and the local Roblox API key are processed or stored on your device. Account-linked features, authentication, donator records, and other server-side features may involve RoValra servers.
- **Secure Database:** Tokens are stored in a secured, encrypted database. **Roblox User IDs are not encrypted**, as they are public identifiers used to link your account to its specific settings and features.
- **Extension Storage:** Chrome Extension storage is not encrypted by Chrome by default. Do not treat locally stored coordinates or the local Roblox API key as protected against other software or users who can access your browser profile or device.
- **Token Sensitivity:** Tokens are never shared with third parties.
- **No IP Storage:** We do not store your IP address in our database.
- **HTTPS:** All API interactions are secured via encrypted HTTPS tunnels.

<!-- section:third-party-services:fas fa-cloud -->
## Third-Party Services

To provide its features, RoValra interacts with several Application Programming Interfaces (APIs):

- **Roblox's APIs:** Essential for the platform interaction and OAuth.
- **RoValra APIs:** Managed by the developer to handle donator records and data support.
- **Cloudflare:** All traffic is routed through Cloudflare for performance and DDoS protection.
- **Infrastructure:** Standard web traffic information, including IP addresses, may be processed by Cloudflare to establish secure connections, provide performance and DDoS protection, and operate the service. RoValra does not intentionally store IP addresses in its own application database. Cloudflare's own processing and retention are governed by its policies and configuration.

<!-- section:data-retention:fas fa-history -->
## Data Retention

- **General Users:** User IDs and usernames are retained while needed to maintain persistent settings and server-side features.
- **Donators:** IDs and RoValra oauth tokens are retained while needed to maintain authentication, badge status, and donator benefits, unless erasure is requested or a longer period is required for security or legal obligations.
- **Discord connections:** A connected Discord user ID may be retained while it is needed to associate donator status with the applicable Discord role, unless removal is requested.
- **Local data:** Location coordinates, settings, cached data, and the local Roblox API key remain in Extension storage until the relevant feature removes them, the user clears the Extension's data, or the Extension is uninstalled. Chrome controls the exact deletion behavior.
- **After uninstalling:** Uninstalling the Extension removes its locally stored browser data according to the browser's extension-storage behavior, but does not automatically delete data already stored on RoValra servers. Server-side settings, including user-set statuses, may remain and may continue to be visible to other RoValra users who use the Extension until they expire, are removed, or deletion is requested.

<!-- section:children-privacy:fas fa-child -->
## Children's Privacy

RoValra does not ask users for their age and does not have enough information to determine which users are under 13. As a result, a user under 13 may use the Extension and RoValra may store that user's Roblox User ID, username, account-linked settings, and other information described in this policy when necessary to provide the Extension's features. We do not use age as a basis for selectively allowing or refusing these ordinary features.

We do not knowingly request information from children for purposes unrelated to providing RoValra's features. If a parent or guardian believes that a child has provided personal information to RoValra, they may contact **RoValraContact@gmail.com** to request access to or deletion of the child's data. We will review and handle the request according to applicable law. This section describes our current practices and is not a statement of legal compliance in any particular jurisdiction.

<!-- section:changes:fas fa-sync-alt -->
## Changes to This Privacy Policy

We may update this Privacy Policy from time to time. Any changes will be posted on this page, and we will update the “Effective Date.” Your continued use of the Extension after any changes signifies your acceptance of the new policy.

<!-- section:contact-information:fas fa-envelope -->
## Contact Information

If you have any questions or concerns about this Privacy Policy, you can contact us at:

RoValraContact@gmail.com