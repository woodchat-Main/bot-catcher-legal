# Privacy Policy for Bot Catcher

> **Note:** This policy is subject to change. For material changes affecting data handling or user rights, an updated policy will be published here and/or announced in the support Discord server.

**Official instance info**

This Privacy Policy applies only to the official Bot Catcher Discord bot, operated by woodchat. Bot Catcher is currently only run as a single instance operated by woodchat. It is not distributed for self-hosting; if that ever changes, this policy will be updated to say so.

See also: [Terms of Service](TERMS.md)

**Last Updated: July 3, 2026**

woodchat operates the Bot Catcher Discord bot. This Privacy Policy explains what data the bot collects, stores, and uses.

## Information We Collect

Bot Catcher stores data in a Supabase (PostgreSQL) cloud database. Supabase acts as our infrastructure provider and stores data on our behalf; see [Third-Party Processors](#third-party-processors) below.

**Server configuration**, per server the bot is added to:
- Server ID, server name, staff/log channel IDs, rejoin invite URL
- Feature toggles and settings (honeypot, account age check, link detection, mass message detection, thresholds, timeout durations, configured actions)
- Honeypot channel IDs and names
- Immune role IDs and names, and the ID of the admin who added them

**Catch records**, created when the bot takes action against a user:
- Server ID, channel ID, message ID, the user's Discord ID and username/tag
- The text content of the specific message that triggered the catch, and any attachment URLs and SHA256 hashes of that message
- Which action was taken (kick, ban, timeout, warn) and why

**Action log**: a history of every moderation action taken (server ID, user ID and tag, moderator ID if a human triggered it, action, reason, feature, timestamp).

**Image data for spam detection**: when an image triggers the honeypot, is added via `/blacklist add`, or is submitted to the global blacklist, we store:
- A SHA256 hash of the image (not the image file itself)
- ORB feature descriptors: a mathematical representation of the image's visual keypoints, used for fuzzy/perceptual matching. This is derived data, not a copy of the image, and cannot be used to reconstruct the original image.
- We do not keep a permanent copy of the original image file. Images are downloaded in memory to compute hashes/descriptors and, when a catch is reported to a staff/log/dev channel, are re-uploaded to that Discord channel as part of the alert (see "Where Catch Data Is Sent" below); we do not separately archive the image files ourselves.

**Suspicious links**: a shared list of known phishing/scam domains (domain name, category, who reported it, report count). Not tied to any individual server or user beyond the reporter's ID.

**Message fingerprints (ephemeral)**: to detect the same message or image spammed across multiple channels, we briefly store a hash of message content/attachments per server, channel, and user. This data is automatically deleted approximately every 5 minutes and is not retained.

## How We Use Your Information

This data powers the bot's core functions:
- Monitor honeypot channels and detect account age, phishing links, mass-posted spam, and known bad images
- Execute the configured moderation action (kick, ban, timeout, or warn) and DM the affected user
- Post catch details to your server's staff/log channels, including a "Submit to Global Blacklist" option for staff to use at their discretion
- Maintain a shared blacklist of spam images and phishing domains across all servers running the bot (see "Cross-Server Data Sharing" below)
- Provide admins with `/viewcatches`, `/actionlog`, and `/checkperms` to review what the bot has done in their own server

## Where Catch Data Is Sent

**Cross-server data sharing (global blacklist):** Bot Catcher's spam detection is more effective when servers share intelligence about known bad actors. Because of this:
- If a submitted image's SHA256 hash or ORB descriptors are found in 3 or more separate servers, the hash/descriptors are automatically promoted to a **global blacklist entry** shared across every server running the bot. Staff can also manually submit a specific catch to the global blacklist via a button on the catch alert.
- Only the hash and derived ORB descriptors are shared globally, never the original image file, message content, or the identity of the user who posted it.
- Known phishing/scam domains are shared globally by design (this is a shared blocklist, not server-specific).

**Operator visibility (dev log channel):** if configured, every catch across every server (server name and ID, channel, the offending user's ID and username, the triggering message content, any attachment images, the action taken, and reason) is also posted to a private Discord channel operated by woodchat, used to monitor the bot's health, review false positives, and decide whether to promote images to the global blacklist. This means the bot operator can see catch details, including message content and images, from any server running the bot. This channel is not visible to server admins or members of other servers.

## Data Storage and Retention

Data is stored in our Supabase (PostgreSQL) database and retained until you remove it or remove the bot. Removing the bot from your server does not currently trigger automatic deletion of that server's data (unlike some smaller single-purpose bots) because catch history, action logs, and blacklist entries are used across the service and for cross-server protection. If you want your server's data deleted after removing the bot, contact us using the details in [Contact](#contact) and we will delete it on request.

Ephemeral message fingerprints (used for mass-message detection) are deleted automatically approximately every 5 minutes regardless of whether the bot is still in your server.

## What We Do Not Collect

- Full member lists or server-wide activity outside of messages that trigger a detection feature
- Private messages sent to the bot by users, or voice data
- IP addresses or payment/account details
- The original file of an image once its hash/descriptors have been extracted (we do not maintain a separate image archive beyond what is posted to configured alert channels as part of a catch)

## Third-Party Processors

Bot Catcher relies on the following third-party infrastructure to operate:
- **Discord**: all bot activity happens through Discord's API. [Discord's Privacy Policy](https://discord.com/privacy) applies to your use of Discord itself.
- **Supabase**: our database provider, used to store all persistent data described above.

No data is sold or shared with any third party beyond what's described in this policy (Discord, Supabase as our processor, and the cross-server sharing described above).

## Your Rights

Server admins can view their server's catches and action history at any time via `/viewcatches` and `/actionlog`, and remove specific blacklist entries via `/blacklist remove`. To request deletion of your server's data, or to ask what data we hold about a specific user or server, contact us (see [Contact](#contact)).

## Contact

For support or privacy requests, join the support Discord server: https://discord.gg/NDfWd4qJU7
