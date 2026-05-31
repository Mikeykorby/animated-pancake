# 🥞 Animated Pancake - AI Chatbot Pro v5.0

[![Latest Release](https://img.shields.io/github/v/release/Mikeykorby/animated-pancake?color=56B4F8&label=Latest&style=for-the-badge)](https://github.com/Mikeykorby/animated-pancake/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Mikeykorby/animated-pancake/total?color=56B4F8&style=for-the-badge)](https://github.com/Mikeykorby/animated-pancake/releases)
[![License](https://img.shields.io/github/license/Mikeykorby/animated-pancake?color=A855F7&style=for-the-badge)](LICENSE)
[![Last Updated](https://img.shields.io/github/last-commit/Mikeykorby/animated-pancake?color=34D399&label=Updated&style=for-the-badge)](https://github.com/Mikeykorby/animated-pancake/commits/main)

> **The Ultimate AI-Powered Chatbot for Roblox with Cinematic UI & Multi-Provider Support**

---

## 📖 Table of Contents

- [About The Project](#-about-the-project)
- [Features](#-features)
- [Demo](#-demo)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [API Setup](#-api-setup)
- [Usage](#-usage)
- [Releases](#-releases)
- [Changelog](#-changelog)
- [Roadmap](#-roadmap)
- [About Me](#-about-me)
- [Support](#-support)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## ✨ About The Project

**Animated Pancake** is an advanced AI chatbot system designed for Roblox games, featuring a stunning MacLib-powered UI with smooth animations, tab navigation, and support for multiple AI providers (Ollama, Gemini, Groq, Hugging Face).

Built with performance and aesthetics in mind, this chatbot listens to in-game chat and responds intelligently using your choice of AI backend, complete with conversation memory and customizable behavior.

### 🔥 Why Choose Animated Pancake?

- **First of its kind** - Original creation with unique features
- **MacLib UI Integration** - Beautiful, modern interface with cinematic animations
- **Multi-AI Support** - Switch between 4 different AI providers instantly
- **Smart Memory System** - Remembers conversations for contextual responses
- **Highly Configurable** - Tweak every aspect to your needs
- **Active Development** - Regular updates and new features

---

## 🚀 Features

### UI Improvements (v5.0)
- ✅ **MacLib UI Library** integration for premium look and feel
- ✅ **Tab Navigation** - Seamless switching between Main, Settings, and Credits
- ✅ **Cinematic Animations** - Smooth transitions with easing functions
- ✅ **Real-time Status Updates** - Live indicators for AI state and message count
- ✅ **Modern Color Palette** - Professional dark theme with accent colors
- ✅ **Toast Notifications** - Clean, non-intrusive feedback system
- ✅ **Draggable Window** - Reposition the UI anywhere on screen
- ✅ **Responsive Design** - Adapts to different screen sizes

### Core Features
- 🤖 **Multi-AI Provider Support**
  - Ollama (Local)
  - Google Gemini
  - Groq (Ultra-fast)
  - Hugging Face (Local or API)
- 💾 **Conversation Memory** - Configurable history retention
- 🎯 **Smart Filtering** - Whitelist/Blacklist system
- 📏 **Range Detection** - Optional proximity-based responses
- ⚡ **Fast Response Times** - Optimized API calls
- 🔒 **Secure API Keys** - Password-protected input fields
- 📊 **Live Statistics** - Message counter and provider display
- ⚙️ **In-Game Settings** - Configure without restarting

---

## 🎬 Demo

![Demo GIF](https://via.placeholder.com/600x300/0f172a/56B4F8?text=AI+Chatbot+Demo+Coming+Soon)

*Watch the chatbot in action with smooth UI animations and real-time AI responses!*

---

## 📦 Installation

### Method 1: Direct Download (Recommended)

1. Go to the [Releases Page](https://github.com/Mikeykorby/animated-pancake/releases)
2. Download the latest `.lua` file
3. Open Roblox Studio
4. Open the **Script** editor
5. Paste the entire code
6. Configure your API keys (see [Configuration](#-configuration))
7. Press **Play** to test!

### Method 2: Git Clone (Developers)

```bash
# Clone the repository
git clone https://github.com/Mikeykorby/animated-pancake.git

# Navigate to directory
cd animated-pancake

# Copy the script to your Roblox project
# (Open the .lua file and paste into Roblox Studio)
```

### Requirements

- **Roblox Studio** (Latest version)
- **API Key** from one of the supported providers:
  - [Google Gemini](https://makersuite.google.com/app/apikey) (Recommended for beginners)
  - [Groq](https://console.groq.com/keys) (Fastest response times)
  - [Ollama](https://ollama.ai/) (Local, no API key needed)
  - [Hugging Face](https://huggingface.co/settings/tokens) (Advanced users)

---

## ⚙️ Configuration

### Quick Setup

Find this section at the top of the script:

```lua
local CFG = {
    GEMINI_API_KEY = "YOUR_GEMINI_API_KEY_HERE",
    GROQ_API_KEY = "YOUR_GROQ_API_KEY_HERE",
    AI_PROVIDER = 0,  -- 0=Ollama, 1=Gemini, 2=Groq, 3=HuggingFace
    MAX_MEMORY = 30,
    AI_ACTIVE = true,
    CLOSE_RANGE_ONLY = true,
    MAX_STUDS = 11,
    SHOW_PREFIX = true,
}
```

### Configuration Options

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `GEMINI_API_KEY` | String | `""` | Your Google Gemini API key |
| `GROQ_API_KEY` | String | `""` | Your Groq API key |
| `AI_PROVIDER` | Number | `0` | AI provider (0-3) |
| `MAX_MEMORY` | Number | `30` | Max messages to remember per user |
| `AI_ACTIVE` | Boolean | `true` | Enable/disable AI on startup |
| `CLOSE_RANGE_ONLY` | Boolean | `true` | Only respond to nearby players |
| `MAX_STUDS` | Number | `11` | Maximum distance for responses |
| `MIN_CHARS` | Number | `1` | Minimum message length |
| `MAX_CHARS` | Number | `200` | Maximum message length |
| `SHOW_PREFIX` | Boolean | `true` | Show player name before responses |
| `NAME_FORMAT` | String | `"P"` | Name format pattern |
| `NAME_SEPARATOR` | String | `","` | Separator between name and message |

### Whitelist & Blacklist

```lua
local WHITELIST = { seem2006 = true }  -- Only these users (if CLOSE_RANGE_ONLY = false)
local BLACKLIST = { Builderman = true }  -- Never respond to these users
```

---

## 🔑 API Setup

### Google Gemini (Recommended)

1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click **Create API Key**
4. Copy the key and paste it in `GEMINI_API_KEY`
5. Set `AI_PROVIDER = 1`

**Pros:** Free tier available, easy setup, good quality  
**Cons:** Rate limits on free tier

### Groq (Fastest)

1. Visit [Groq Console](https://console.groq.com/keys)
2. Create an account or sign in
3. Generate a new API key
4. Copy the key and paste it in `GROQ_API_KEY`
5. Set `AI_PROVIDER = 2`

**Pros:** Extremely fast, generous free tier  
**Cons:** Requires account setup

### Ollama (Local)

1. Download from [Ollama.ai](https://ollama.ai/)
2. Install and run: `ollama run cogito:8b`
3. Ensure local server is running on port 11434
4. Set `AI_PROVIDER = 0` (no API key needed)

**Pros:** Completely free, private, no rate limits  
**Cons:** Requires local setup, uses your hardware

### Hugging Face (Advanced)

1. Get a token from [Hugging Face Settings](https://huggingface.co/settings/tokens)
2. For local: Set up inference server at `http://localhost:5000`
3. Set `AI_PROVIDER = 3`
4. Configure `HF_LOCAL_URL` if using local

**Pros:** Access to many models, flexible  
**Cons:** More complex setup

---

## 🎮 Usage

### In-Game Controls

1. **Open UI** - The UI opens automatically when the script starts
2. **Toggle AI** - Click the big blue/purple button to enable/disable AI
3. **Settings** - Click "Settings" to access configuration options
4. **Change Provider** - Use the dropdown in Settings to switch AI providers
5. **Adjust Memory** - Use the slider to change memory limit (1-100)
6. **Reset Memory** - Clear all conversation history

### Commands

The chatbot responds automatically to chat messages based on your configuration. No special commands needed!

**Special Phrase:** Say `"what did i just say"` to test the memory system.

### Tips

- Keep the UI visible to monitor AI status
- Use Settings to fine-tune behavior without restarting
- Check toast notifications for important updates
- Stay within range (if `CLOSE_RANGE_ONLY = true`) for responses

---

## 📦 Releases

### Current Release: v5.0 (Latest)

**Release Date:** January 2025  
**Status:** ✅ Stable

#### Downloads

- [📥 Download Latest Release](https://github.com/Mikeykorby/animated-pancake/releases/latest)
- [📚 View All Releases](https://github.com/Mikeykorby/animated-pancake/releases)
- [🌿 Browse Main Branch](https://github.com/Mikeykorby/animated-pancake/tree/main)

#### Version History

| Version | Release Date | Status | Changes |
|---------|--------------|--------|---------|
| **v5.0** | Jan 2025 | ✅ Current | MacLib UI, Tabs, Animations |
| v4.0 | Dec 2024 | ⚠️ Legacy | Single window, basic settings |
| v3.0 | Nov 2024 | ❌ Deprecated | Initial multi-provider support |
| v2.0 | Oct 2024 | ❌ Deprecated | Memory system added |
| v1.0 | Sep 2024 | ❌ Deprecated | First public release |

[📝 View Detailed Release Notes](https://github.com/Mikeykorby/animated-pancake/releases)

---

## 🔄 Changelog

### v5.0 - Major UI Overhaul (Current)

#### UI Improvements
- ✨ Complete rewrite using **MacLib UI Library**
- 🎨 Modern tabbed interface (Main, Settings, Credits)
- 🎬 Cinematic slide animations between tabs
- 📱 Responsive design with proper scaling
- 🎯 Dropdown menus for provider selection
- 📊 Real-time statistics dashboard
- 🔔 Enhanced toast notification system
- 🖱️ Improved draggable window mechanics

#### Features Added
- ➕ Credits tab with contributor information
- ➕ Password-protected API key inputs
- ➕ Slider controls for numerical values
- ➕ Live message counter
- ➕ Provider status indicator
- ➕ Elastic toggle animations
- ➕ Auto-save configuration changes

#### Performance
- ⚡ Reduced code size by 30%
- ⚡ Faster UI rendering
- ⚡ Optimized animation loops
- ⚡ Better memory management

### v4.0 - Single Window Design

- Unified UI in single frame
- Tab navigation system
- Hero status card
- Settings panel
- Toggle buttons with hover effects

### v3.0 - Multi-Provider Support

- Added Gemini integration
- Added Groq integration
- Added Hugging Face support
- Provider switching mechanism

### v2.0 - Memory System

- Conversation history tracking
- Contextual responses
- Memory limit configuration
- Reset functionality

### v1.0 - Initial Release

- Basic AI chatbot functionality
- Ollama integration
- Simple UI
- Chat filtering

---

## 🛣️ Roadmap

### v5.1 - Coming Soon

- [ ] Voice message support
- [ ] Custom response presets
- [ ] Advanced filter rules
- [ ] Multiple language support
- [ ] Theme customization
- [ ] Export/import configurations

### Future Plans

- [ ] Web dashboard for remote management
- [ ] Plugin system for extensibility
- [ ] Analytics dashboard
- [ ] Cloud sync for settings
- [ ] Mobile companion app
- [ ] Discord integration

**Have a feature request?** [Open an Issue](https://github.com/Mikeykorby/animated-pancake/issues) or join the discussion!

---

## 👤 About Me

**Hey! I'm Mikeykorby** 👋

The creator and maintainer of **Animated Pancake**. I'm passionate about combining AI technology with gaming experiences to create innovative tools for the Roblox community.

### 🎯 My Mission

> "To push the boundaries of what's possible in Roblox by integrating cutting-edge AI solutions with beautiful, user-friendly interfaces."

### 🔗 Connect With Me

- **GitHub:** [@Mikeykorby](https://github.com/Mikeykorby)
- **Roblox:** [Mikeykorby](https://www.roblox.com/users/Mikeykorby/profile)
- **Discord:** Join our community server (coming soon!)

### 📬 Contact

- **Issues:** [Report a bug](https://github.com/Mikeykorby/animated-pancake/issues)
- **Discussions:** [Feature requests & help](https://github.com/Mikeykorby/animated-pancake/discussions)
- **Email:** Available via GitHub

---

## 🆘 Support

### Getting Help

1. **Check the Documentation** - Most questions are answered in this README
2. **Search Issues** - Someone may have had the same problem
3. **Open an Issue** - Use the appropriate template
4. **Join Discussions** - Community help and feature requests

### Common Issues

#### "AI failed (401)"
- **Cause:** Invalid API key
- **Solution:** Double-check your API key in Settings

#### "Rate limit exceeded"
- **Cause:** Too many requests
- **Solution:** Wait a few minutes or upgrade your API plan

#### "No response from AI"
- **Cause:** AI provider offline or network issue
- **Solution:** Check your internet connection and provider status

#### "UI not showing"
- **Cause:** Script not running or errors in output
- **Solution:** Check Roblox Studio output for errors

### Bug Report Template

When reporting bugs, please include:

```markdown
**Describe the bug**
A clear description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. See error

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain.

**Environment:**
- Roblox Studio version:
- AI Provider used:
- Script version:

**Additional context**
Add any other context about the problem here.
```

### Feature Request Template

```markdown
**Is your feature request related to a problem?**
A clear description of what the problem is.

**Describe the solution you'd like**
What you want to happen.

**Describe alternatives you've considered**
Other solutions you've thought about.

**Additional context**
Any other details or mockups.
```

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### Terms of Use

✅ **You can:**
- Use this project for personal projects
- Modify the code for your own use
- Learn from the codebase
- Report bugs and suggest features

❌ **You cannot:**
- Claim this work as your own original creation
- Remove attribution or watermarks
- Sell this project without significant modifications
- Harass or abuse the developer

**Note:** This is an original creation. Unauthorized copying or plagiarism will be addressed appropriately.

---

## 🙏 Acknowledgments

Special thanks to:

- **[MacLib Creator](https://brady-xyz.gitbook.io/maclib-ui-library)** - For the amazing UI library
- **[Google](https://ai.google.dev/)** - For Gemini AI
- **[Groq](https://groq.com/)** - For ultra-fast inference
- **[Ollama](https://ollama.ai/)** - For local AI capabilities
- **[Hugging Face](https://huggingface.co/)** - For open-source AI models
- **The Roblox Community** - For inspiration and support
- **All Contributors** - Everyone who has helped improve this project

---

## 📊 Stats

[![GitHub Stars](https://img.shields.io/github/stars/Mikeykorby/animated-pancake?style=for-the-badge&color=FBBF24)](https://github.com/Mikeykorby/animated-pancake/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/Mikeykorby/animated-pancake?style=for-the-badge&color=56B4F8)](https://github.com/Mikeykorby/animated-pancake/network/members)
[![GitHub Issues](https://img.shields.io/github/issues/Mikeykorby/animated-pancake?style=for-the-badge&color=EF4444)](https://github.com/Mikeykorby/animated-pancake/issues)
[![GitHub Pull Requests](https://img.shields.io/github/issues-pr/Mikeykorby/animated-pancake?style=for-the-badge&color=34D399)](https://github.com/Mikeykorby/animated-pancake/pulls)

---

<div align="center">

**Made with ❤️ by Mikeykorby**

⭐ **Star this repo if you find it useful!** ⭐

[Report Bug](https://github.com/Mikeykorby/animated-pancake/issues) · [Request Feature](https://github.com/Mikeykorby/animated-pancake/discussions) · [View Releases](https://github.com/Mikeykorby/animated-pancake/releases)

**Version:** v5.0 | **Last Updated:** January 2025

</div>

