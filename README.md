<p align="center">
  <a href="https://balagraphics.github.io/yt-viewer-panel/">
    <img src="files/button.svg" width="520" alt="PowerShell Installer" />
  </a>
</p>

<div align="center">
<img src="assets/banner.png" width="100%" alt="Youtube Viewer Bot banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-4fe3e3?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-4F46E5?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-EA580C?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=9B59B6&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Yt+Viewer+Panel+Pro;%E2%9C%A8+Automate+Everything;%F0%9F%92%A1+Community+Tested;%F0%9F%94%A7+Zero+Setup+Required;%E2%AD%90+Active+Development+2026;%F0%9F%9A%80+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=nodejs" />
  <img src="https://skillicons.dev/icons?i=windows" />
  <img src="https://skillicons.dev/icons?i=discord" />
  <img src="https://skillicons.dev/icons?i=github" />
</p>

---

You've already tried the YouTube view bots that die after 200 hits and leave your watch-time graph looking like a flatline. **yt-viewer-panel** is the PowerShell-driven panel I actually keep on my desktop — it manages viewer sessions, watch-time pacing, and rotating proxy pools without the babysitting.

---

## System Requirements

| Component | Minimum | Notes |
|---|---|---|
| OS | Windows 10 / 11 (x64) | 22H2+ recommended |
| PowerShell | 5.1+ | PowerShell 7.x works too |
| .NET | 4.8 runtime | Bundled on modern Win10/11 |
| Network | Stable broadband | Residential proxies strongly advised |
| Browser | Edge / Chrome installed | Headless session driver uses it |
| Disk | ~250 MB free | Logs + session cache |

---

## Features

- **Session orchestration** — spin up N concurrent viewer sessions with per-session cookie isolation, so YouTube's dedup heuristics don't collapse your count
- **Watch-time pacing** — configurable retention curves (30s / 60s / full-video) instead of the obvious "skip at 0:05" pattern that gets flagged instantly
- **Proxy pool rotation** — plug in HTTP/SOCKS5 lists, auto-rotate per session, health-check dead nodes before they burn a view
- **Referrer + UA spoofing** — randomize referrer chains and user agents so traffic doesn't look like it spawned from one machine
- **Rate limiter** — global and per-session throttles to stay under YouTube's velocity triggers (you know the ones)
- **Live dashboard** — PowerShell-hosted local panel showing views submitted, retention %, proxy health, and ban/soft-block counters
- **Retention analytics** — CSV export of per-session watch duration for tuning curves without re-running blind
- **Playlist + search-term targeting** — point sessions at specific video IDs, playlists, or keyword-discovered results
- **Session replay logs** — timestamped logs of every request, so when a batch gets soft-blocked you can see exactly where

---

## What Is yt-viewer-panel?

A Windows PowerShell toolkit + local web panel for managing YouTube viewer sessions. Not a SaaS, not a "cloud view service" — it runs on your box and drives headless browser sessions through a proxy pool you control.

---

## Comparison: this vs. what's actually out there

| Tool | Session isolation | Watch-time curves | Proxy rotation | Local panel | Bypass hardening |
|---|---|---|---|---|---|
| **yt-viewer-panel** | ✅ per-session cookies | ✅ configurable | ✅ auto + health-check | ✅ PowerShell-hosted | ✅ UA/referrer spoof |
| YTViewBooster (classic) | ⚠️ shared jar | ❌ fixed 10s | ❌ manual | ❌ | ❌ |
| ViewKick scripts | ⚠️ partial | ⚠️ preset only | ✅ | ❌ | ⚠️ |
| Generic "yt-bot" gists | ❌ | ❌ | ❌ | ❌ | ❌ |
| Browser-farm setups | ✅ | ✅ custom | ✅ | ❌ manual | ✅ but heavy |

The gists die on first detection. ViewKick gets you numbers but no dashboard. The browser-farm route works but eats 8 GB of RAM — this panel keeps sessions lean.

---

## How it works

1. Open PowerShell as your normal user (no admin needed for the framework itself).
2. Paste the one-line command from the landing page — it pulls the PowerShell Core bootstrap, verifies the signature, and drops the panel runtime into `%LOCALAPPDATA%\yt-viewer-panel`.
3. Launch the panel — it opens a local dashboard in your default browser (default `http://localhost:7077`).
4. Drop in your proxy list, set session count + retention curve, paste target video IDs or search terms, hit start.
5. Watch the counters. Tune the rate limiter when soft-blocks tick up — that's the whole game.

No `.exe` installer, no bundled junk — the bootstrap only writes to your user profile.

---

## Compatibility

- **Windows 10 22H2 / 11** — primary target, tested on current platform builds (Q1 2026)
- **Server 2022** — works, headless session driver needs the browser installed manually
- **WSL2** — unsupported for session driving (browser driver is Win32-bound); proxy management works
- **Offline** — panel loads and proxy lists are editable offline; sessions obviously require network
- **PowerShell Core 7.x** — supported alongside PS 5.1

---

## FAQ

**🔄 Does the panel auto-update?**
Yes — the bootstrap checks the landing for the current panel build on launch. You can pin a version by setting `YTV_PANEL_PIN` in the env if you don't want surprise changes mid-batch.

**🚫 Am I going to get banned?**
Accounts used purely as viewers can get flagged — that's the nature of the game. Partition accounts, don't reuse the same Google account across batches, and pace aggressively. Proxies help more than anything else.

**🎮 Does it touch Steam / games?**  
No — this is strictly YouTube view-management tooling. Nothing to do with Steam or game processes.

**🔒 Do I need a VPN?**  
Not strictly, but combined with a residential proxy pool you'll see far better retention of counted views. Datacenter proxies get soft-blocked fast.

**⚙️ Can I run it headless on a VM?**  
Yes, but the browser driver sticks to Win32. A Windows VM works; a bare Linux box does not.

**📊 Why do views max out around 60–70% of submitted sessions?**  
YouTube's dedup filters what looks synthetic. That ceiling is normal — retention curve + proxy quality is what moves it. Anyone promising 100% is selling you something.

**💬 PowerShell says "running scripts is disabled".**  
`Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` — the bootstrap only needs that scope. Don't set it machine-wide for one tool.

---

## Disclaimer

Provided for **educational and research purposes only**. Using this against YouTube violates their Terms of Service and can result in channel strikes or IP bans. You are solely responsible for how you run it and what you point it at. The author assumes no liability for account, financial, or legal consequences.

---

## License

MIT — see `LICENSE`. Use at your own risk.
