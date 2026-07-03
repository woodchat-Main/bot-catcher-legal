# Terms of Service for Bot Catcher

> **Note:** This policy is subject to change. For material changes affecting data handling or user rights, an updated policy will be published here and/or announced in the support Discord server.

**Official instance info**

These Terms of Service apply only to the official Bot Catcher Discord bot, operated by woodchat. Bot Catcher is currently only run as a single instance operated by woodchat. It is not distributed for self-hosting; if that ever changes, these terms will be updated to say so.

See also: [Privacy Policy](PRIVACY.md)

**Last Updated: July 3, 2026**

## Acceptance of Terms

Adding Bot Catcher to your Discord server means you agree to these Terms of Service.

## Description of Service

Bot Catcher is an automated anti-spam and anti-bot moderation tool. It monitors for honeypot channel triggers, new-account behavior, phishing links, mass-posted spam, and known bad images, and takes a configured moderation action (kick, ban, timeout, or warn) against offending users.

## Required Permissions

Depending on which features you enable, the bot may need:
- View Channels and Send Messages (to monitor channels and post logs/warnings)
- Kick Members / Ban Members / Moderate Members (Timeout) (to execute moderation actions)
- Manage Messages (to delete spam across channels)

`/checkperms` audits your server for missing permissions and role hierarchy issues.

## Prohibited Uses

Do **not** use Bot Catcher to:
- Violate Discord's Terms of Service, or cause the bot to do so
- Target or harass specific users, or configure the bot to punish users in a discriminatory or deceptive way
- Evade moderation in other servers
- Configure a commonly used channel (e.g. `#general`) as a honeypot with the intent of causing mass, indiscriminate punishment
- Submit images to the global blacklist that are not actually spam/malicious content, or otherwise abuse shared cross-server features in bad faith

Server administrators are solely responsible for how they configure the bot, including which channels are monitored, what actions are taken, and any custom invite links or messages the bot sends on their behalf.

## Bot Operator Commitment

Only server administrators (or users they grant permission to) can change the settings the bot uses within their own server. The bot operator will not intentionally reconfigure a server's settings in a harmful way or circumvent the administrators' intentions. All configuration changes are a direct result of administrator actions taken through `/setup` and related commands.

The bot operator (woodchat) retains cross-server visibility as described in the Privacy Policy (dev log channel, global blacklist), and may act on that data, for example promoting or removing a global blacklist entry, or reaching out about misuse, but does not alter a server's own configuration without the server's administrators doing so themselves.

## User Responsibilities

For the purposes of this policy, "administrator" means any Discord server owner, administrator, or person granted permission to configure the bot. "Member" means any user in a Discord server where Bot Catcher is installed.

Administrators are responsible for:
- Ensuring the bot's role is positioned above members' highest roles and has the permissions needed for the actions they configure;
- Reviewing catch and action logs (`/viewcatches`, `/actionlog`) for accuracy, including false positives from fuzzy image matching;
- Not configuring honeypot channels, immune roles, or automated actions in ways that are deceptive, harmful, or cause mass disruption to their own members;
- Communicating to their members, where appropriate, that automated moderation is in use.

Any misuse, misconfiguration, or failure to understand the consequences of a chosen setup is the sole responsibility of the administrator who configured it.

The bot operator is not liable for any actions taken against members as a result of the bot's automated enforcement, including kicks, bans, timeouts, or warnings, whether triggered correctly or as a false positive. All server members are subject to the configuration choices made by their server's administrators.

## Limitation of Liability

Bot Catcher is provided "as is" without warranties of any kind. We are not responsible for false positives or false negatives in spam/bot detection, Discord API outages or limitations, permission or role-hierarchy errors preventing an action from completing, or data loss arising from platform or infrastructure problems.

## Termination

You may remove the bot from your server at any time to stop it acting in that server. See the Privacy Policy for how removal affects stored data. We may remove the bot from, or refuse service to, servers that violate these terms.

## Governing Law

Disputes are governed by the laws of the United Kingdom.

## Contact

For support, join the support Discord server: https://discord.gg/NDfWd4qJU7
