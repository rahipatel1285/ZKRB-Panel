<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Platform-Windows%20|%20macOS%20|%20Linux%20|%20Android-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Interface-GUI%20+%20CLI-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/API-REST%20+%20GraphQL-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge" />
</p>

# ZKRB Panel

> A cross-platform GitHub API interaction toolkit for developers and researchers managing multiple GitHub accounts. Built with both a modern GUI (CustomTkinter) and a lightweight CLI — automatically selects the right interface based on your environment.

ZKRB Panel simplifies repetitive GitHub API workflows for developers, maintainers, and QA engineers who work with multiple GitHub accounts. Instead of manually switching between accounts in a browser, ZKRB Panel provides a single unified dashboard to perform common GitHub operations across all your accounts simultaneously.

> **Note:** This is a closed-source, encrypted application. The distributed `main.py` is obfuscated/encrypted and not human-readable. Source code is not available for inspection or modification.

---

## Use Cases

- **Project Maintainers** — Manage organization bot accounts, quickly star/watch repositories across team accounts, and coordinate engagement on new projects.
- **QA & DevOps Engineers** — Test GitHub webhook integrations, issue tracking pipelines, and CI/CD workflows by creating realistic test data (issues, comments, forks) across multiple test accounts.
- **API Researchers** — Study GitHub's REST and GraphQL API behavior, rate limiting, and response patterns at scale.
- **Developer Advocacy Teams** — Coordinate engagement across official team accounts for product launches and community initiatives.

---

## Features

### Account Operations

| Feature | Description | API |
|---------|-------------|-----|
| Follow / Unfollow User | Manage following relationships across accounts | GraphQL |
| Star / Unstar Repository | Add or remove stars on repositories | GraphQL |
| Fork Repository | Fork a repository to multiple accounts | REST |
| Create Issue | Open issues on any accessible repository | REST |
| Auto-Comment | Post templated comments on open issues | REST |
| Token Validator | Verify token health, scopes, and linked usernames | REST |

### Technical Highlights

- **Dual Interface** — Full GUI with CustomTkinter (splash screen, sidebar navigation, real-time stats, activity log) and a terminal-based CLI for headless environments
- **Smart Environment Detection** — Automatically detects display availability, SSH sessions, Termux, and falls back to CLI when no GUI is possible
- **GitHub API v4 (GraphQL)** — Uses GitHub's modern GraphQL API for efficient mutations with automatic node ID resolution
- **Retry & Rate-Limit Handling** — Exponential backoff with configurable retries; respects API rate limits
- **Token Management** — Loads tokens from CSV, validates each on startup, filters accounts that have already performed an action (skip-if-done logic)
- **Device-Bound Licensing** — Hardware-fingerprinted activation for secure license enforcement
- **Protection System** — Server-side target protection prevents actions on specified accounts/repositories
- **Single-File Architecture** — Entire application in one `main.py` — no submodules, no complex project structure

---

## Supported Platforms

| Platform | GUI | CLI | Auto-Detected |
|----------|:---:|:---:|:---:|
| Windows 10/11 | ✅ | ✅ | GUI |
| macOS | ✅ | ✅ | GUI |
| Linux (Desktop) | ✅ | ✅ | GUI |
| Linux (Server / SSH) | — | ✅ | CLI |
| Termux (Android) | — | ✅ | CLI |
| WSL | — | ✅ | CLI |

---

## Prerequisites

- **Python 3.10** or later
- **pip** (Python package manager)
- **GitHub Personal Access Tokens** with appropriate scopes
- **Activation Key** (required for first-time setup)

---

## Quick Start

### 1. Download & Install

Download the latest release and extract it:

```bash
cd ZKRB-Panel
pip install -r requirements.txt
```

### 2. Generate GitHub Personal Access Tokens (PATs)

Each GitHub account you want to use needs its own token:

1. Log in to [github.com](https://github.com) → **Settings** → **Developer settings**
2. Navigate to **Personal access tokens** → **Tokens (classic)**
3. Click **Generate new token (classic)**
4. Name it (e.g., `zkrb-panel`), set No expiration, and select All scopes
5. Click **Generate token** and copy it immediately

> **Security Note:** Tokens are stored locally in `tokens.csv` and are never hardcoded. Add `tokens.csv` to `.gitignore` before pushing to any remote repository.

### 3. Configure Tokens

Add your tokens to `tokens.csv` (one per line):

```csv
ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
ghp_yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
ghp_zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
```

### 4. Run

```bash
python main.py
```

The application automatically selects GUI or CLI based on your environment. To force CLI mode, run from an SSH session or a system without a display server.

---

## Activation

A license key is required on first launch. The key is bound to your device hardware fingerprint.

- **Single-device** — One key, one machine
- **Persistent** — Survives reboots, stored in encrypted local auth file
- **Heartbeat** — Periodic license verification with server

### Get a Key

Contact on Telegram: **[@dk_gz](https://t.me/dk_gz)**

---

## Project Structure

```
ZKRB-Panel/
├── main.py            # Encrypted application (GUI + CLI)
├── tokens.csv         # Your GitHub PATs (one per line)
├── requirements.txt   # Python dependencies
└── README.md
```

---

## How It Works

```
┌──────────────────────────────────────────────┐
│              ZKRB Panel (Encrypted)          │
├──────────────────────────────────────────────┤
│  1. Detects your environment automatically   │
│  2. Launches GUI (desktop) or CLI (terminal) │
│  3. Activates with your license key          │
│  4. Loads tokens from tokens.csv             │
│  5. Executes GitHub operations in parallel   │
├──────────────────────────────────────────────┤
│  GUI Mode              │  CLI Mode           │
│  ├── Splash screen     │  ├── Menu system    │
│  ├── Sidebar nav       │  ├── ANSI coloring  │
│  ├── Stat cards        │  ├── Interactive I/O │
│  ├── Progress bar      │  └── Summary reports │
│  └── Activity log      │                     │
└──────────────────────────────────────────────┘
```

---

## Security & Privacy

- **Encrypted Source** — Application code is obfuscated and encrypted; not readable or modifiable
- **Local Token Storage** — Tokens stay in `tokens.csv` on your machine, never uploaded or shared
- **Encrypted Auth** — License file (`.dk_auth`) uses device-specific key derivation
- **HTTPS Only** — All GitHub API calls use encrypted connections
- **No Telemetry** — No analytics or data collection beyond license heartbeat
- **Target Protection** — Server-side system prevents accidental actions on protected accounts/repos

---

## Legal & Compliance

### Disclaimer

This software is developed for **educational purposes, API research, and authorized account management workflows**. It is intended for use with GitHub accounts that you own or have explicit authorization to manage.

Users are solely responsible for ensuring their usage complies with:
- [GitHub Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service)
- [GitHub Acceptable Use Policies](https://docs.github.com/en/site-policy/acceptable-use-policies/github-acceptable-use-policies)
- All applicable local laws and regulations

The developers assume **no liability** for misuse of this software or any consequences arising from usage that violates third-party terms of service.

### Responsible Use Guidelines

1. Only use tokens from accounts you own or are authorized to manage
2. Respect GitHub's rate limits and API usage policies
3. Do not use this tool to artificially inflate engagement metrics
4. Do not target accounts or repositories without authorization
5. Use the built-in delay system to avoid excessive API load

---

<p align="center">
  <b>Developed by DK</b><br>
  <sub>© 2026 DK — All Rights Reserved</sub>
</p>
