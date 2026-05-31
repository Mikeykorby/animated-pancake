# 🥞 Animated Pancake - AI Chatbot Pro v5.1

> **Next-Gen Roblox AI Chatbot with Cinematic UI & Multi-Provider Support**

[![Version](https://img.shields.io/github/v/release/Mikeykorby/animated-pancake?label=Latest%20Release&color=blue)](https://github.com/Mikeykorby/animated-pancake/releases)
[![License](https://img.shields.io/github/license/Mikeykorby/animated-pancake?color=green)](LICENSE)
[![Stars](https://img.shields.io/github/stars/Mikeykorby/animated-pancake?style=social)](https://github.com/Mikeykorby/animated-pancake/stargazers)
[![Forks](https://img.shields.io/github/forks/Mikeykorby/animated-pancake?style=social)](https://github.com/Mikeykorby/animated-pancake/network/members)
[![Last Updated](https://img.shields.io/github/last-commit/Mikeykorby/animated-pancake?color=orange)](https://github.com/Mikeykorby/animated-pancake/commits/main)

---

## 📖 Table of Contents

- [About](#about)
- [Features](#features)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Releases](#releases)
- [Roadmap](#roadmap)
- [Support](#support)
- [About Me](#about-me)
- [License](#license)

---

## 🎯 About

**Animated Pancake** (AI Chatbot Pro) is an advanced, cinematic AI chatbot system for Roblox games. It features a modern tabbed UI powered by MacLib, supports multiple AI providers (Ollama, Gemini, Groq, Hugging Face), and includes intelligent memory management, proximity detection, and real-time status updates.

Perfect for enhancing player engagement with automated, context-aware responses!

---

## ✨ Features

### 🎨 UI Improvements (v5.1)
- **MacLib Integration**: Sleek, modern tabbed interface
- **Cinematic Animations**: Smooth transitions between tabs
- **Real-time Status**: Live indicators for AI activity
- **Responsive Design**: Adapts to different screen sizes
- **Dark Theme**: Easy on the eyes with accent colors

### 🚀 Core Features
- **Multi-Provider Support**: Switch between Ollama, Gemini, Groq, and Hugging Face
- **Smart Memory**: Contextual conversation history (configurable limit)
- **Proximity Detection**: Only respond to nearby players (optional)
- **Whitelist/Blacklist**: Fine-tune who the bot interacts with
- **Custom Prefixes**: Personalize response formatting
- **Rate Limiting**: Built-in debounce to prevent spam
- **Error Handling**: Graceful fallbacks for API failures

---

## 📦 Installation

### Option 1: Direct Download
1. Go to [Releases](https://github.com/Mikeykorby/animated-pancake/releases)
2. Download the latest `.lua` file
3. Paste into your Roblox game's `ServerScriptService` or `StarterPlayerScripts`

### Option 2: Clone Repository
```bash
git clone https://github.com/Mikeykorby/animated-pancake.git
cd animated-pancake
```

### Option 3: Roblox Studio
1. Open Roblox Studio
2. Create a new `LocalScript` in `StarterPlayerScripts`
3. Copy the contents of `src/AIChatbotPro.lua`
4. Configure API keys in the script

---

## ⚙️ Configuration

Edit the `CFG` table at the top of the script:

```lua
local CFG = {
    GEMINI_API_KEY = "YOUR_GEMINI_API_KEY_HERE",
    GROQ_API_KEY = "YOUR_GROQ_API_KEY_HERE",
    AI_PROVIDER = 0,              -- 0: Ollama, 1: Gemini, 2: Groq, 3: HF
    MAX_MEMORY = 30,              -- Messages to remember per user
    AI_ACTIVE = true,             -- Start enabled
    CLOSE_RANGE_ONLY = true,      -- Only respond to nearby players
    MAX_STUDS = 11,               -- Max distance for responses
    SHOW_PREFIX = true,           -- Show player name in responses
    NAME_SEPARATOR = ",",         -- Separator for name prefix
}
```

### API Keys Setup
- **Gemini**: Get key at https://makersuite.google.com/app/apikey
- **Groq**: Get key at https://console.groq.com/keys
- **Ollama**: Run locally at http://localhost:11434
- **Hugging Face**: Set up local endpoint or use hosted API

---

## 🎮 Usage

### In-Game Controls
- **Toggle AI**: Click the main button to enable/disable
- **Settings Tab**: Adjust memory, provider, range, and more
- **Credits Tab**: View project info and links

### Commands
- Type normally in chat - the bot will auto-respond
- Use `#` prefix to exclude messages from processing
- Ask "what did i just say" to test memory

---

## 📬 Releases

### Current Release: v5.1
- **Date**: May 2024
- **Status**: ✅ Stable
- **Download**: [Latest Release](https://github.com/Mikeykorby/animated-pancake/releases/latest)

### Version History

| Version | Date       | Status  | Highlights                          |
|---------|------------|---------|-------------------------------------|
| v5.1    | May 2024   | ✅ Latest | MacLib UI, organized repo, credits  |
| v5.0    | May 2024   | ✅ Stable | Tab navigation, cinematic animations|
| v4.0    | Apr 2024   | ⚠️ Deprecated | Single window design              |
| v3.0    | Mar 2024   | ❌ Legacy | Basic chatbot functionality         |

[View All Releases →](https://github.com/Mikeykorby/animated-pancake/releases)

---

## 🗺️ Roadmap

### v5.1 (Current)
- ✅ MacLib UI integration
- ✅ Repository organization
- ✅ Credits tab
- ✅ Enhanced documentation

### v5.2 (Upcoming)
- 🔄 Web dashboard for remote management
- 🔄 Plugin system for custom commands
- 🔄 Analytics dashboard
- 🔄 Voice message support

### Future Plans
- Multi-language support
- Custom AI model training
- Discord webhook integration
- Player behavior analytics

---

## 🆘 Support

### Getting Help
1. Check the [Issues](https://github.com/Mikeykorby/animated-pancake/issues) page
2. Start a [Discussion](https://github.com/Mikeykorby/animated-pancake/discussions)
3. Join our Discord (link in About Me)

### Bug Report Template
```markdown
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior.

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment:**
- Roblox Studio version
- AI Provider used
- Script version
```

---

## 👤 About Me

**Hey! I'm seem2006** 👋

A passionate developer focused on integrating AI into gaming experiences. I love building tools that enhance player engagement and create immersive interactions.

### 🔗 Connect With Me
- **Discord**: `seem2006` (add me!)
- **Roblox**: [Profile](https://www.roblox.com/users/123456789/profile) *(update with your ID)*
- **GitHub**: [@Mikeykorby](https://github.com/Mikeykorby)
- **Portfolio**: Coming soon!

### 💡 My Mission
Making AI accessible and fun for Roblox developers everywhere. Every line of code is crafted with performance and user experience in mind.

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### Terms of Use
✅ **You can:**
- Use in personal and commercial projects
- Modify and distribute
- Contribute improvements

❌ **You cannot:**
- Claim as your own original work
- Remove attribution
- Use for malicious purposes

---

## 🙏 Acknowledgments

- **MacLib**: For the amazing UI library
- **Google Gemini**: AI provider
- **Groq**: Fast inference API
- **Ollama**: Local AI runner
- **Community**: All contributors and testers

---

## 📊 Stats

![GitHub Stars](https://img.shields.io/github/stars/Mikeykorby/animated-pancake?style=social)
![GitHub Forks](https://img.shields.io/github/forks/Mikeykorby/animated-pancake?style=social)
![GitHub Issues](https://img.shields.io/github/issues/Mikeykorby/animated-pancake)
![GitHub Pull Requests](https://img.shields.io/github/issues-pr/Mikeykorby/animated-pancake)

---

<div align="center">

**Made with ❤️ by seem2006**

[⬆ Back to Top](#-animated-pancake---ai-chatbot-pro-v51)

</div>
