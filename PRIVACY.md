# Privacy Policy for Bot Catcher

> **Note:** This policy is subject to change. For material changes affecting data handling or user rights, an updated policy will be published here and/or announced in the support Discord server.

**Official instance info**

This Privacy Policy applies only to the official Bot Catcher Discord bot and its website, https://botcatcher.cc (including the dashboard), both operated by woodchat. Bot Catcher is currently only run as a single instance operated by woodchat. It is not distributed for self-hosting; if that ever changes, this policy will be updated to say so.

See also: [Terms of Service](TERMS.md)

**Last Updated: October 16, 2026**

woodchat operates the Bot Catcher Discord bot and its website. This Privacy Policy explains what data the bot and the website collect, store, and use.

## Information We Collect

Bot Catcher stores data in a database (SQLite) on a server operated by woodchat and hosted by Contabo. Contabo provides that server and stores the data on our behalf; see [Third-Party Processors](#third-party-processors) below.

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

**Settings history**: when a server's settings change through `/setup` or the dashboard, we record who changed them (Discord user ID and username), which setting changed with its old and new value, and when. It is kept for up to a year, at most 10,000 entries per server, and is deleted together with the server's data.

**Image data for spam detection**: when an image triggers the honeypot, is added via `/blacklist add`, or is submitted to the global blacklist, we store:
- A SHA256 hash of the image (not the image file itself)
- A perceptual hash: a short summary of the image's overall structure, used to recognize resized or re-saved copies
- ORB feature descriptors and the positions of those features in the image: a mathematical representation of the image's visual keypoints, used for fuzzy matching. This is derived data, not a copy of the image, and cannot be used to reconstruct the original image.
- A 64x64 pixel grayscale thumbnail. Unlike the items above, this is a very small, low resolution picture of the image. It is kept only so that improvements to image matching can be tested against images that were already caught. It is never posted to Discord or shown to any server.
- Apart from that thumbnail, we do not keep a copy of the original image file. Images are downloaded in memory to compute the data above and, when a catch is reported to a staff/log/dev channel, are re-uploaded to that Discord channel as part of the alert (see "Where Catch Data Is Sent" below); we do not separately archive the image files ourselves.

When staff or the operator mark a catch as a false positive, the same kinds of image data are stored for that image as a known clean entry, so it is not flagged again.

**Vote records**: voting for Bot Catcher on top.gg unlocks a custom honeypot warning and extra honeypot channels. To check a vote, your Discord user ID is sent to top.gg. If you have voted, we store your user ID, when you last voted, and how many of your votes we have seen, so the bot can tell you when you last voted. Voting never affects any protection feature.

**Suspicious links**: a shared list of known phishing/scam domains (domain name, category, who reported it, report count). Not tied to any individual server or user beyond the reporter's ID.

**Website sign in (dashboard)**: you can sign in at botcatcher.cc with your Discord account to view and change Bot Catcher's settings for servers you manage. Discord asks you to allow two things: your account's basic details and the list of servers you are in. From that, and while you are signed in, we store:
- Your Discord user ID, username, display name and avatar, and whether your account has two-factor authentication turned on
- The servers you are in, with their names, icons, IDs and your permissions there, used to show the servers you can open and to check your access
- The login tokens Discord gives us, encrypted, used only to refresh that server list and confirm you are still a member
- Your browser's user agent, and when you signed in and were last active, so a session can expire

This is kept in a separate database used only for sign in. It is never included in backups. A session ends when you sign out, after 7 days without use, or 30 days after you signed in, whichever comes first, and it is then deleted. Signing out also asks Discord to cancel the login tokens. You can also remove Bot Catcher under Authorized Apps in your Discord settings at any time.

The website sets one cookie to keep you signed in and, only for the few minutes a sign in takes, a second cookie that protects the sign in from tampering. Both are strictly necessary; there are no advertising, analytics or tracking cookies. Your choice of colour theme is saved in your own browser and never sent to us.

The public pages show three totals across all servers (servers using the bot, spam bots caught, shared scam images). They contain nothing about any individual server or user.

If your browser blocks, or would block, part of a page for security reasons, the page may send us a short technical report: the rule involved, the file name, a few characters of the blocked content, and the page path with any server IDs removed. It contains nothing about you.

**Message fingerprints (ephemeral)**: to detect the same message or image spammed across multiple channels, we briefly store a hash of message content/attachments per server, channel, and user. A cleanup runs every 5 minutes and removes anything older than the longest detection window a server can configure, which is 1 hour. Nothing is kept beyond that.

**Bug reports**: when you use `/bug`, what you write is posted to a private Discord channel operated by woodchat, together with your Discord user ID and username, the server and channel you sent it from, and the time. It is not stored in our database. It stays in that channel until woodchat deletes it, and you can ask for that at any time (see [Contact](#contact)).

## How We Use Your Information

This data powers the bot's core functions:
- Monitor honeypot channels and detect account age, phishing links, mass-posted spam, and known bad images
- Execute the configured moderation action (kick, ban, timeout, or warn) and DM the affected user
- Post catch details to your server's staff/log channels, including a "Submit to Global Blacklist" option for staff to use at their discretion
- Maintain a shared blacklist of spam images and phishing domains across all servers running the bot (see "Cross-Server Data Sharing" below)
- Provide admins with `/viewcatches`, `/actionlog`, and `/checkperms` to review what the bot has done in their own server
- Let server admins change their server's settings, and staff view them, on the website, with detection statistics, the blacklist, a permissions check and the settings history

## Where Catch Data Is Sent

**Cross-server data sharing (global blacklist):** Bot Catcher's spam detection is more effective when servers share intelligence about known bad actors. Because of this:
- If the same image is blacklisted by 3 or more established servers (servers that have used the bot for at least 30 days, have at least 50 members, and belong to different owners), its image data is automatically promoted to a **global blacklist entry** used across every server running the bot. Images reported by fewer established servers are reviewed by the operator before they can become global. Staff can also manually submit a specific catch to the global blacklist via a button on the catch alert.
- A global entry is used only for matching. Other servers never see it; they only learn that a posted image matched. The original image file, the message content, and the identity of the user who posted it are never shared with other servers.
- Known phishing/scam domains are shared globally by design (this is a shared blocklist, not server-specific).

**Operator visibility (dev log channel):** if configured, every catch across every server (server name and ID, channel, the offending user's ID and username, the triggering message content, any attachment images, the action taken, and reason) is also posted to a private Discord channel operated by woodchat, used to monitor the bot's health, review false positives, and decide whether to promote images to the global blacklist. This means the bot operator can see catch details, including message content and images, from any server running the bot. This channel is not visible to server admins or members of other servers.

## Data Storage and Retention

Data is stored in our database on the Contabo hosted server and retained until you remove it or remove the bot. Removing the bot from your server does not currently trigger automatic deletion of that server's data (unlike some smaller single-purpose bots) because catch history, action logs, and blacklist entries are used across the service and for cross-server protection. If you want your server's data deleted after removing the bot, contact us using the details in [Contact](#contact) and we will delete it on request.

Ephemeral message fingerprints (used for mass-message detection) are deleted automatically within about an hour, by a cleanup that runs every 5 minutes, regardless of whether the bot is still in your server.

**Backups**: the database is backed up every 6 hours. Backups are kept on the same server for up to 14 days and then deleted automatically. A copy of each backup is also sent to a private Discord channel operated by woodchat so the data survives a server failure. Those copies are encrypted before they leave the server, and the key needed to read them is kept offline by woodchat. Data you ask us to delete is gone from the backups on the server within 14 days. The encrypted copies in the private channel cannot be read without the offline key. Website sign in data is never backed up.

## What We Do Not Collect

- Full member lists or server-wide activity outside of messages that trigger a detection feature
- Private messages sent to the bot by users, or voice data
- Stored IP addresses: the website uses your IP address only in memory, for a short time, to stop abusive request rates, and never writes it down
- Payment or account details
- The original file of an image once the image data described above has been extracted (we do not maintain an image archive beyond the small grayscale thumbnail described above and what is posted to configured alert channels as part of a catch)

## Third-Party Processors

Bot Catcher relies on the following third-party infrastructure to operate:
- **Discord**: all bot activity happens through Discord's API. [Discord's Privacy Policy](https://discord.com/privacy) applies to your use of Discord itself.
- **Contabo**: hosts the server the bot and its database run on. All persistent data described above is stored there.
- **top.gg**: when a vote is checked, your Discord user ID is sent to top.gg. [top.gg's Privacy Policy](https://top.gg/privacy) applies to voting there.
- **Cloudflare**: every visit to the website passes through Cloudflare, which provides the secure connection and protection against attacks. Cloudflare sees your IP address and the request as it passes. [Cloudflare's Privacy Policy](https://www.cloudflare.com/privacypolicy/) applies to that processing.

No data is sold or shared with any third party beyond what's described in this policy (Discord, Contabo as our hosting provider, top.gg for vote checks, Cloudflare for website traffic, and the cross-server sharing described above).

## Your Rights

Server admins can view their server's catches and action history at any time via `/viewcatches` and `/actionlog`, see its settings history on the website, and remove specific blacklist entries via `/blacklist remove`. You can end your website session at any time by signing out, which deletes it. To request deletion of your server's data, or to ask what data we hold about a specific user or server, contact us (see [Contact](#contact)).

## Contact

For support or privacy requests, join the support Discord server: https://discord.gg/NDfWd4qJU7
