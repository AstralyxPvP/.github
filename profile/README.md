![AstralyxPvP Logo](https://www.astralyxpvp.int.yt/Assets/logo.png)

# AstralyxPvP

![Minecraft](https://img.shields.io/badge/Minecraft-Java_1.9+-00aa00?style=for-the-badge)
![Discord](https://img.shields.io/badge/Discord-Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Workers-+-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)
![D1](https://img.shields.io/badge/Database-D1_SQLite-F6822E?style=for-the-badge&logo=sqlite&logoColor=white)
![Paper](https://img.shields.io/badge/Plugin-Paper_1.21-e34c26?style=for-the-badge)
![Made in India](https://img.shields.io/badge/Made_in-India_🇮🇳-FF9933?style=for-the-badge)

**A competitive India-based 1.9+ FFA Minecraft PvP network where everything runs on XP** — no coins, no pay-to-win. Every player starts at **0 XP**, staff included. Grind it, level up, risk it, and prove it.

We build the whole stack in-house — websites, Discord bots, Cloudflare Workers, and Paper plugins.

## 📦 Public repositories

### 🎮 [AstralyxXP](https://github.com/AstralyxPvP/AstralyxXP)
**The XP & Levels system — the heart of the network.**
- Cloudflare Worker bot with a **D1 (SQLite)** database, serving all Discord slash commands: `/daily`, `/balance`, `/leaderboard`, `/coinflip`, `/slots`, `/transfer`, plus staff `/setxp` `/addxp` `/removexp`.
- **XP minigames** that fire when chat spikes: Raining XP, Guess the answer, Fallen XP, Ladders, Luck Duck.
- **Paper plugin** (`AstralyxXP.jar`) so players can view, claim, gamble, and trade XP right in-game — with Discord account linking (`/linkaccount` + `/xp bind`), unlinked Minecraft-only grinding, and smart XP merging (higher side wins).
- 50 levels, daily streaks, live D1 leaderboards. Every push to `main` auto-deploys via GitHub Actions → wrangler.

### 🕸️ [AstralyxPvP-site](https://github.com/AstralyxPvP/AstralyxPvP-site)
**The official website** (hosted on Cloudflare Pages at `www.astralyxpvp.int.yt`).
- Vanilla HTML/CSS/JS landing page for the network with live leaderboards and ELO tracking.
- **[AstralyxAI](https://www.astralyxpvp.int.yt/astralyxai)** — an integrated AI chat assistant powered by **Google Gemini**, protected by **Cloudflare Turnstile**.

### 🤖 [AstralyxAI](https://github.com/AstralyxPvP/AstralyxAI)
**The network's AI worker.**
- Cloudflare Worker with **native Gemini Tool Calling** and a full **staff role hierarchy**.
- Ties into **live leaderboards**, **real server status**, and answers community questions on Discord.

### 🛡️ [AstralyxPvP-Rank-Plugin](https://github.com/AstralyxPvP/AstralyxPvP-Rank-Plugin)
**The rank plugin for Paper servers.**
- Full rank system synced to online custom API servers — ships configured for our setup, easy to tweak for yours.

### 🧹 [Laxmi](https://github.com/AstralyxPvP/Laxmi)
*(a.k.a. DesiBot)*
- A **Discord AutoMod bot** that keeps the community channels clean.

### 📰 [AstralyxNews](https://github.com/AstralyxPvP/AstralyxNews)
- The network's news feed — announcements & updates.

### 💬 [AstralyxForums](https://github.com/AstralyxPvP/AstralyxForums)
- Community forums frontend.

### 🔎 [AstralyxAssistant](https://github.com/AstralyxPvP/AstralyxAssistant)
- Assistant tooling for the network.

### 📶 [astralyx-status](https://github.com/AstralyxPvP/astralyx-status)
- Network **status page** — uptime tracking for the server & services.

### 🌐 [astralyxpvp.github.io](https://github.com/AstralyxPvP/astralyxpvp.github.io)
- Legacy GitHub Pages site.

### 🏠 [.github](https://github.com/AstralyxPvP/.github)
- This org profile & community health files.

## ⚔️ How XP works

- **Grind it** — claim `/daily`, win minigames, stay active.
- **Level up** — 50 levels (level 1 = 100 XP) unlock ranks & cosmetics.
- **Risk it** — bet XP on `/coinflip` and `/slots`.
- **Prove it** — land on the `/leaderboard`.
- **Take it in-game** — the Paper plugin links your Discord XP straight into the server.

## 🌐 Get in

<div align="center">

**Server IP:** `java.astralyxpvp.int.yt`

[![Discord](https://img.shields.io/badge/Join_Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/u8BFrpRwEg)
[![Website](https://img.shields.io/badge/Visit_Website-0088cc?style=for-the-badge&logo=globe&logoColor=white)](https://www.astralyxpvp.int.yt)
[![YouTube](https://img.shields.io/badge/YouTube-@AstralyxPvP-red?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@AstralyxPvP)

</div>

---

© NebulaGames 2026. Not affiliated with Mojang.