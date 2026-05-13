> **🔒 This is a public mirror of a private repository.**
> The full source code lives in a private monorepo. If you're interested in viewing or contributing,
> please email **[support@nextquest.dev](mailto:support@nextquest.dev)** with a short introduction.

<div align="center" style="background-color:#011627;padding-top:16px">
  <img src="https://raw.githubusercontent.com/dangervalentine/NextQuestREADME/main/next_quest_readme.png" alt="NextQuest Logo" width="128" height="128" style="border-radius: 50%; border: 1px solid white;"/>
  <h1 style="color:#D6DEEB">NextQuest</h1>
  <p style="color:#D6DEEB">Track what you're playing. Plan what's next. Remember what you've finished.</p>
</div>

<p align="center">
  <a href="https://nextquest.dev"><img src="https://img.shields.io/badge/web-nextquest.dev-1d9bf0.svg" alt="Web"></a>
  <a href="https://apps.apple.com/app/id6751153491"><img src="https://img.shields.io/badge/App%20Store-iOS-000000.svg?logo=apple" alt="iOS"></a>
  <a href="https://play.google.com/store/apps/details?id=com.dangervalentine.nextquest"><img src="https://img.shields.io/badge/Google%20Play-Android-3DDC84.svg?logo=android" alt="Android"></a>
  <img src="https://img.shields.io/badge/license-All%20Rights%20Reserved-red.svg" alt="License">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/expo-SDK%2055-000020.svg?logo=expo" alt="Expo">
  <img src="https://img.shields.io/badge/react--native-0.83-61DAFB.svg?logo=react" alt="React Native">
  <img src="https://img.shields.io/badge/next.js-16-000000.svg?logo=nextdotjs" alt="Next.js">
  <img src="https://img.shields.io/badge/react-19-61DAFB.svg?logo=react" alt="React">
  <img src="https://img.shields.io/badge/.NET-10-512BD4.svg?logo=dotnet" alt=".NET 10">
  <img src="https://img.shields.io/badge/postgres-17-336791.svg?logo=postgresql" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/elasticsearch-8-005571.svg?logo=elasticsearch" alt="Elasticsearch">
</p>

---

## 🎮 What is NextQuest?

NextQuest is a cross-platform game library, planner, and journal for video games. It runs as a
native **iOS + Android** app and a full-featured **web** companion, backed by a shared API that
serves the same data to both clients. The model is **playthrough-centric** — a single title can
sit in `playing`, `finished`, and `backlog` at the same time across different platforms.

> All game media (screenshots, covers, logos) are the property of their respective publishers and
> appear here for informational and illustrative purposes only.

## 🌐 Where to find it

| Surface | Where |
|---|---|
| Web app | **[nextquest.dev](https://nextquest.dev)** |
| iOS | **[App Store](https://apps.apple.com/app/id6751153491)** |
| Android | **[Google Play](https://play.google.com/store/apps/details?id=com.dangervalentine.nextquest)** |
| Support | [support@nextquest.dev](mailto:support@nextquest.dev) |

---

## ✨ Features

### 📚 Your library
- **Five statuses** — `playing`, `queued`, `backlog`, `finished`, `dropped`, plus an `undiscovered` discovery surface
- **Per-platform playthroughs** — the same game can be `playing` on Switch and `finished` on PC
- **Reviews, ratings, and structured notes** — sectioned, reorderable, and synced across devices
- **Lists** with sharing, comments, and drag-and-drop ordering — including **tier lists** with shareable OG images
- **Favorites, custom collections,** and rich filtering by genre, theme, platform, year, and franchise

### 🔭 Discovery
- Search and browse the full **IGDB** catalog with **Elasticsearch**-powered ranking
- Companion data from **Steam** (player counts, store presence) and metadata pulled nightly
- Franchise and company pages with sortable releases
- **Daily challenges** and **quizzes** built from your own library

### 🕹️ Arcade
- Mini-games built directly into the web app, including a Space Invaders-style cabinet
- Shareable scores and a per-cabinet leaderboard

### 📱 Mobile-first ergonomics
- **Offline-first** — every action writes to local SQLite first and reconciles with the server when the network returns
- **Drag-and-drop** prioritization, swipe gestures, and haptic feedback
- **Deep links** (`https://nextquest.dev/games/...`, `/lists/...`) open natively on installed devices
- **Custom MultiAvatar** identity system — no profile photo required

### 🔐 Account & data
- Sign in with **Google**, **Apple**, or email/password (Firebase Auth)
- One-click **data export** — ZIP of CSVs plus a full-fidelity JSON snapshot of everything you've created
- Privacy-first — your real name is never published; public surfaces use your username only

### 🎨 Design
- Custom **Night Owl OLED** dark theme with aurora layering and accent palette
- Typography: **Outfit** + **FiraCode** + **Press Start 2P** for retro accents
- Responsive layout shared between mobile and web with parity-checked Lucide iconography

---

## 🏗️ Architecture

NextQuest is a single private monorepo with three first-class sub-projects:

| Sub-project | Stack |
|---|---|
| **`app/`** — iOS + Android | Expo SDK 55, React Native 0.83, React 19, TypeScript, Zustand, expo-sqlite, Firebase Auth |
| **`web/`** — Web | Next.js 16 (App Router, RSC), React 19, TypeScript, Zustand, CSS Modules + design-token CSS variables, Firebase Auth |
| **`server/`** — API | ASP.NET Core (.NET 10), minimal APIs, PostgreSQL 17 (raw **Npgsql**, no ORM), Elasticsearch, xUnit + Testcontainers |

### Highlights

- **Two PostgreSQL databases:** a user-data DB (`nextquest`) managed by hand-rolled append-only SQL migrations, and an IGDB catalog DB (`igdb`, ~122 entity types) reseeded nightly at 2 AM CT.
- **Offline-first mobile** — `expo-sqlite` is the source of truth; Zustand projects state from it. A `pending_mutations` queue replays writes on reconnect. Delta `GET /api/sync/{domain}?since=...` endpoints power fast cold-start hydration.
- **Two-layer auth** — an `X-API-KEY` header gates every endpoint by client role (`frontend` vs `super`), with **Firebase JWT** for user-scoped requests on top.
- **Admin tooling bundled into web** — `/admin/{ops,es,users,tools,user-dashboard}` is staff-gated and ships in the same Next.js app.
- **Dockerized infrastructure** — isolated `prod` / `staging` / `test` Compose stacks for Postgres, the API, the web app, Elasticsearch, and Kibana.
- **Standalone Next.js build** baked into a multi-stage Dockerfile; the API runtime image carries `pg_dump` / `pg_restore` for schema utilities.

---

## 🗺️ Game status model

| Status | Meaning |
|---|---|
| 🎯 `playing` | Active playthrough — only one per platform at a time |
| 📅 `queued` | Up next, scheduled to start |
| 📚 `backlog` | Owned or wishlisted, not yet started |
| ⭐ `finished` | Completed (a game can be finished on one platform and playing on another) |
| 🚩 `dropped` | Started and abandoned |
| 🔍 `undiscovered` | Not in your library yet — surfaced through search and recommendations |

Each playthrough carries its own status, rating, review, notes, dates, and platform.

---

## 🤝 Contributing

The full source is private. If you're interested in viewing the code, working on the project, or
discussing a feature, email **[support@nextquest.dev](mailto:support@nextquest.dev)** with a short
introduction.

## 📄 License

**All Rights Reserved.** This project and its source code are proprietary and confidential. No part
of this software may be reproduced, distributed, or transmitted in any form without prior written
permission of the author.

## 🙏 Acknowledgments

- 🎮 **[IGDB](https://www.igdb.com/)** — primary game metadata
- 🕹️ **[Steam](https://store.steampowered.com/)** — supplemental store + player data
- 🎨 **[Night Owl Theme](https://github.com/sdras/night-owl-vscode-theme)** — visual inspiration
- 🛠️ **[Expo](https://expo.dev/)**, **[Next.js](https://nextjs.org/)**, and the React Native + .NET communities

---

<p align="center"><b>Happy questing. 🎮✨</b></p>
