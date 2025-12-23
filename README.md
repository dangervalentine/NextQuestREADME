> **🔒 This is a private repository.**  
> Access to the full source code is restricted.  
> If you’re interested in viewing or contributing to this project, please email **[support@nextquest.dev](mailto:support@nextquest.dev)** with a short message introducing yourself.

  <div align="center" style="background-color:#011627;padding-top:16px">
    <img src="https://raw.githubusercontent.com/dangervalentine/NextQuestREADME/main/next_quest_readme.png" alt="NextQuest Logo" width="128" height="128" style="border-radius: 50%; border: 1px solid white;"/>
    <h1 style="color:#D6DEEB">NextQuest</h1>
  </div>

[![Platform](https://img.shields.io/badge/platform-expo-blue.svg)](https://expo.dev/)
[![License](https://img.shields.io/badge/license-All%20Rights%20Reserved-red.svg)]()
[![Build](https://img.shields.io/badge/build-android%20%7C%20ios-success)]()
[![React Native](https://img.shields.io/badge/react--native-0.79.5-blue)](https://reactnative.dev/)
[![Expo SDK](https://img.shields.io/badge/expo-53.0.19-000020.svg)](https://expo.dev/)

**NextQuest** is a sophisticated mobile game tracking application built with **React Native** and **Expo**. Manage your gaming journey with a dark, elegant interface inspired by the Night Owl VS Code theme. Track your progress, discover new titles, and curate a rich, personalized game collection.

"All game media (screenshots, covers, logos) are property of their respective publishers and are used here for informational and illustrative purposes only."

---

## ✨ Features

### 🎯 Core Functionality
- 🎮 **Track Game Status**: Ongoing, Backlog, Completed, Undiscovered, Dropped
- 🔍 **Game Discovery**: Search games via **IGDB** and **RAWG** APIs
- ⭐ **Personal Rating**: Rate games 1–10 with visual star-based UI
- 🏷️ **Priority System**: Organize games via drag-and-drop
- 🕹️ **Platform Selection**: Choose from 100+ platforms
- 🧾 **Rich Metadata**: Screenshots, storylines, genres, franchises, and more

### 🎨 User Experience
- 🌌 **Night Owl Theme**: Custom dark mode with accent colors
- 🎞️ **Smooth Animations**: Page transitions, loaders, gestures
- 📳 **Haptics**: Tactile feedback for interactions
- 🔤 **Typography**: Inter, FiraCode, PressStart2P
- 📱 **Responsive Layout**: Fully optimized for mobile
- 📣 **Toasts**: Informative feedback messages

### ⚙️ Technical Features
- 🗃️ **SQLite**: Local relational DB with 20+ tables
- 📦 **React Context**: Efficient global state
- ✋ **Gesture Handling**: Drag/drop, swipe navigation
- 📴 **Offline Support**: Syncs remote data with local storage
- 🖼️ **Custom Splash**: Animated launch screen

---

## 🚀 Quick Start

### 🔧 Requirements
- Node.js ≥ 16
- Expo CLI: `npm install -g expo-cli`
- Android Studio / Xcode (for device testing)
- API keys from:
  - [Twitch Console](https://dev.twitch.tv/console/apps) (IGDB)
  - [RAWG API](https://rawg.io/apidocs)

### 🛠 Installation

```bash
# Clone repository
git clone https://github.com/dangervalentine/NextQuest
cd nextquest

# Install dependencies
npm install

# Configure environment
echo "TWITCH_CLIENT_ID=xxx" >> .env
echo "TWITCH_CLIENT_SECRET=xxx" >> .env
echo "RAWG_API_KEY=xxx" >> .env

# Start development
npm start
```

---

## 🗂️ Project Structure

<details>
<summary><strong>Click to expand</strong></summary>

```
nextquest/
├── src/
│   ├── components/
│   │   ├── common/         # Shared UI
│   │   └── splash/         # Launch screen
│   ├── screens/
│   │   ├── game/
│   │   │   ├── GameDetail/
│   │   │   ├── GameList/
│   │   │   └── shared/
│   │   └── Home.tsx
│   ├── contexts/           # React Contexts
│   ├── data/
│   │   ├── config/         # SQLite setup
│   │   ├── models/         # TypeScript types
│   │   ├── repositories/   # Data access
│   │   └── mappers/        # Raw-to-model
│   ├── services/api/       # API clients
│   ├── navigation/         # Nav configs
│   ├── constants/
│   │   ├── theme/          # Night Owl styling
│   │   └── api/            # Endpoint configs
│   ├── utils/              # Utility functions
│   └── assets/
│       ├── fonts/
│       ├── platforms/
│       └── ESRB/
├── android/
├── config/
├── scripts/
└── app.json
```

</details>

---

## 🎮 Game Status System

Each game can be categorized into one of five statuses:

| Status        | Meaning                            |
|---------------|------------------------------------|
| 🎯 Ongoing     | Currently being played             |
| 📚 Backlog     | Planned for future play            |
| ✅ Completed   | Finished and archived              |
| 🔍 Undiscovered| Available for discovery            |
| ⏸️ Dropped     | Started but no longer active       |

Each category supports:
- Ratings
- Notes
- Priority settings

---

## 🗄️ Database Schema Overview

### 🧩 Core Entities
- `games`, `platforms`, `genres`, `companies`, `franchises`

### 🖼️ Media
- `covers`, `screenshots`, `videos`, `websites`, `age_ratings`

### 🧍 User Data
- `quest_games`, `quest_game_status`

Data is persisted locally using **expo-sqlite**. Sample data is seeded via scripts.

---

## 🔧 API Integrations

### 🎮 IGDB API
- OAuth2 via Twitch
- Provides: game titles, covers, genres, trailers, screenshots, release dates
- Auth flow and rate-limiting handled internally

### 🗃️ RAWG API
- Requires API key
- Adds critic scores, player stats, and extra metadata

---

## 🎨 Theming

Inspired by the [Night Owl](https://github.com/sdras/night-owl-vscode-theme) theme:

---

## 🧱 Key Dependencies

| Category       | Libraries |
|----------------|-----------|
| Core           | React Native, Expo, TypeScript |
| Database       | expo-sqlite, async-storage     |
| Navigation     | react-navigation + stack/tabs |
| UI & Animation | Reanimated, Gesture Handler, Draggable FlatList |
| Styling        | Linear Gradient, Custom Fonts |
| Dev Tools      | Jest, Testing Library, dotenv  |

---

## 🤝 Development

This is a proprietary project with all rights reserved. Development is restricted to authorized contributors only.

### For Authorized Contributors
- Write tests for new features
- Follow the existing code style
- Update documentation as needed
- Test on both Android and iOS

### Internal Development Guidelines
- All changes must be approved by the project maintainer
- Follow the established branching strategy
- Ensure proper testing before commits
- Document any new features or changes

---

## 📄 License

**All Rights Reserved**

This project and its source code are proprietary and confidential. No part of this software may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the author.

For licensing inquiries, please contact the project maintainer.

---

## 🙏 Acknowledgments

- 🎨 [Night Owl Theme](https://github.com/sdras/night-owl-vscode-theme) — visual design
- 🎮 [IGDB](https://www.igdb.com/) — metadata provider
- 📦 [RAWG.io](https://rawg.io/) — discovery and review source
- ⚙️ [Expo](https://expo.dev/) — mobile dev toolkit
- 👾 React Native Community — invaluable libraries

---

## 💡 Support

For authorized users experiencing issues:
1. ✅ Check internal documentation
2. 📄 Ensure `.env` keys are set correctly
3. 📚 Read inline comments + this README
4. 🐛 Contact the project maintainer for support

---

**Happy Gaming! 🎮✨**
