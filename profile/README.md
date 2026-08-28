![AstralyxPvP Logo](https://www.astralyxpvp.int.yt/Assets/logo.png)

# AstralyxPvP

![Minecraft](https://img.shields.io/badge/Minecraft-Java_1.9+-00aa00?style=for-the-badge)
![Discord](https://img.shields.io/badge/Discord-Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Workers-+-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)
![D1](https://img.shields.io/badge/Database-D1_SQLite-F6822E?style=for-the-badge&logo=sqlite&logoColor=white)
![Paper](https://img.shields.io/badge/Plugin-Paper_1.21-e34c26?style=for-the-badge)
![Made in India](https://img.shields.io/badge/Made_in-India_🇮🇳-FF9933?style=for-the-badge)

**A competitive India-based 1.9+ FFA Minecraft PvP network where everything runs on XP** — no coins, no pay-to-win. Every player starts at **0 XP**, staff included. Grind it, level up, risk it, and prove it.

We build the whole stack in-house — websites, Discord bots (moderation + AI), Cloudflare Workers, D1 databases, and Paper plugins.

---

## 🎮 [AstralyxXP](https://github.com/AstralyxPvP/AstralyxXP) — the XP & Levels system

**The heart of the network.** A full-stack gamification platform that rewards grinding instead of wallets.

### 🖥️ Cloudflare Worker + D1 database (`src/`)
- **Discord slash commands**: `/daily`, `/balance`, `/leaderboard`, `/coinflip`, `/slots`, `/transfer`, and staff `/setxp` `/addxp` `/removexp`.
- **50 levels** — level 1 = 100 XP, thresholds rise as you climb. Every player starts at 0, staff included.
- **Daily streaks** — claim `/daily` every 24h; consecutive streaks grow the reward.
- **XP minigames** that fire when chat activity spikes (10+ messages/minute):
  - 🌧️ **Raining XP** — XP falls in chat, first to claim it wins.
  - ✨ **Guess the answer** — trivia for XP.
  - 💸 **Fallen XP** — dropped XP to grab.
  - 🪜 **Ladders** — climb-the-message-ladder event.
  - 🦆 **Luck Duck** — pure-luck payout.
- **Staff hierarchy** — role-ID-based grants/strips, nobody excluded from zero.

### 🏗️ Paper plugin (`paper-plugin/`)
- In-game commands for **linked** (Discord-synced) and **unlinked** (Minecraft-only) players: `/xp`, `/balance`, `/daily`, `/coinflip`, `/slots`, `/transfer`, `/leaderboard`.
- **Account linking**: `/xp link` + `/linkaccount` (private flow) and `/xp bind <discordId>` (manual, overrides linkaccount).
- **Unlinked grinding** — Minecraft-only XP that never syncs to Discord.
- **Smart merge** — link later and the higher of your Minecraft/Discord XP wins (`/api/merge` keeps `max`).

### ⚙️ DevOps
- GitHub Actions auto-deploys to Cloudflare on every push to `main`.
- Makefile + npm scripts (`make dev`, `make deploy`, `make test`, `make plugin`…) — 21/21 unit checks green.

---

## 🕸️ [AstralyxPvP-site](https://github.com/AstralyxPvP/AstralyxPvP-site) — the official website

Cloudflare Pages site at **www.astralyxpvp.int.yt**, a full multi-page platform:

- **Home** (`index.html`) — landing page with JSON-LD GameServer + FAQ structured data, SEO-verified (Google, Bing).
- **Live leaderboard** (`leaderboard.html`) + **Hall of Fame** — real ELO standings.
- **AstralyxAI chat** (`astralyxai.html`) — website chat assistant powered by **Google Gemini**, protected by **Cloudflare Turnstile**.
- **Store / vote / apply / rules / support / contact / terms / privacy** — the full network front-end.
- **Cloudflare Functions** (`functions/`):
  - `chat.js` — HMAC-SHA256 **session-token ("VIP pass")** auth so only verified humans hit the AI; Turnstile fallback, optional audio transcription.
  - `news-api.js`, `annoucments.js` — D1-backed web announcements.
  - `forum-api.js`, `discord-callback.js` — forums + Discord OAuth.
  - `audio.js` — media routing.
- Deployed with `wrangler.jsonc`, D1 bound as `DB`.

---

## 🛡️ [Laxmi](https://github.com/AstralyxPvP/Laxmi) — DesiBot, the moderation engine

A full **custom AutoMod + welcome + ticket bot** for the AstralyxPvP Discord (Cloudflare Worker + KV). Built by **IndianCoder3**.

### 🧠 Smart detection (layered)
- **Layer 1** — regex + curated word list covering **English, Hindi and Hinglish** (incl. leetspeak "f u c k" and zero-width char bypasses).
- **Raid detection** — identical messages from 3+ users in 10s = raid.
- **Layer 2** — **Gemini AI classification** (`gemini-3.5-flash-lite`) for the borderline stuff (subtle ads, staff impersonation, NSFW, hate) with structured JSON + confidence.

### ⚖️ Punishments (graduated)
- Delete message → **Dyno `/warn`** → logs infractions in **KV** → **timeout/mute** → **kick** → **ban** → unban — with escalation on repeat offenses.
- **Full moderation toolkit**: `/warn`, `/mute`, `/unmute`, `/kick`, `/ban`, `/unban`, plus staff `/ignore-add` `/ignore-remove` `/ignore-user`.
- **Smart exemptions** — staff never auto-banned; link-posting exempts ≠ swear-word exempts; ignored channels/users; role-based.
- **Infraction history** per user (KV-backed), punishment **DMs** explaining why + how to appeal.
- **Welcome system** — auto role selector for notification roles (announcements/giveaways/tournaments/polls).
- **Ticket system** — "Open Support Ticket" button → forum thread flow → staff alerts.
- **Alert staff** — sends @-mention alerts to staff channels for violations.
- **Gateway** (`gateway.js`) — a separate Node.js (Render) gateway that reads ALL messages and forwards them to the Worker via bearer secret.

---

## 🤖 [AstralyxAI](https://github.com/AstralyxPvP/AstralyxAI) — the AI companion

Cloudflare Worker with **native Gemini Tool Calling** (`gemini-2.5-flash`), fully integrated with the network.

### 💬 Discord commands
- `/chat <message>` — talk to the AI companion (supports context memory per channel, deferred responses).
- `/lb [gamemode]` — ELO leaderboards for **Sword FFA**, **Mace FFA**, **Netherite Pot FFA**.
- `/elostats <player>` — a player's ELO across all gamemodes.
- `/mconline` — live Minecraft server status.
- `/reset` — clear conversation memory.
- `/aiban` `/aiunban` — staff-restrict individual users from the AI.

### 🪄 Real-time tools
- **Live leaderboards**, **player ELO stats**, **server online status** — fetched straight from the API and fed into the model's tool calls, so the AI answers with *real* numbers, not guesses.
- **Staff hierarchy** — full 17-rank role hierarchy guards what the AI can do.
- Another deploy of this code powers the **website AstralyxAI chat** (Gemini + Turnstile).

---

## 💬 [AstralyxForums](https://github.com/AstralyxPvP/AstralyxForums) — community forums

A modern **React + Vite** forum platform:

- **Auth** — Discord OAuth login (`discord-callback`), email verification flow.
- **Pages** — Categories → Subcategories → Threads → Thread detail + **User profiles**.
- **Moderation UI** — staff modals, report modal, ignore-list modal, shadow-edit/delete via `canModerateRole()` role-rank checks.
- **Rich posts** — Markdown rendering (`marked`), markdown toolbar, share modal, avatar canvas.
- **Turnstile** — bot-protected forms.
- **Backed by the `forum-api` Cloudflare Worker** (D1) at `forum-api.chessmrbeaston.workers.dev`.

---

## 🔎 [AstralyxAssistant](https://github.com/AstralyxPvP/AstralyxAssistant) — the fast automod worker

The lightweight sibling of Laxmi — a single-file Cloudflare Worker that:
- **Normalizes** text (Unicode NFD + leetspeak + zero-width char stripping).
- Flags **banned English/Hindi/Hinglish words**, **Discord invite spam**, and **staff impersonation**.
- **Raid detection** (identical messages, 3+ users, 10s window).
- **Gemini layer-2 classifier** for borderline content.
- Deletes messages + triggers **Dyno `/warn`**, logs rich embeds to a mod channel, respects ignored channels and staff exemptions.
- Ships with `gateway.js` (Render-side Discord gateway forwarding to the worker) and a wrangler config.

---

## 📰 [AstralyxNews](https://github.com/AstralyxPvP/AstralyxNews) — news & updates

The network's news announcements. *(Currently seeding the repo with license + initial content.)*

---

## 📶 [astralyx-status](https://github.com/AstralyxPvP/astralyx-status) — the status page

Live service health dashboard (German-locale boilerplate, dark red `#1a0a0a` PvP theme):
- Monitors **5 services** live: Discord Mod Bot, Discord AI Bot, Website, **Minecraft Server**, and **Minecraft Server API**.
- Polls the `uptime-worker.chessmrbeaston.workers.dev` API, shows per-service up/down, latency, next-check countdown, and a **history** section.

---

## 🌐 [astralyxpvp.github.io](https://github.com/AstralyxPvP/astralyxpvp.github.io) — legacy site

The original GitHub Pages site — iframe shell + CNAME + assets, superseded by the Cloudflare Pages site above. Kept for history and the `discord` well-known verification file.

---

## 🏠 [.github](https://github.com/AstralyxPvP/.github)

Org profile + community health files — **this page**.

---

## 🌐 Get in

<div align="center">

**Server IP:** `java.astralyxpvp.int.yt`

[![Discord](https://img.shields.io/badge/Join_Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/u8BFrpRwEg)
[![Website](https://img.shields.io/badge/Visit_Website-0088cc?style=for-the-badge&logo=globe&logoColor=white)](https://www.astralyxpvp.int.yt)
[![YouTube](https://img.shields.io/badge/YouTube-@AstralyxPvP-red?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@AstralyxPvP)

</div>

---

© NebulaGames 2026. Not affiliated with Mojang.