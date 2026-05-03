# 🎮 GTA World Style Nametag Plugin v1.0.0

> High-performance overhead nametag display plugin for FiveM, supporting **ESX** / **QBCore** / **QBox** frameworks

---

## ✨ Features

- 🎯 **GTA World Style** — Displays `Character Name [ID]` above players' heads
- 🔧 **Three Framework Support** — Auto-detects ESX / QBCore / QBox (qbx_core)
- ⚡ **Extreme Performance Optimization** — Dual-thread architecture, zero stuttering
- 📏 **Distance-Based Fade** — Auto fades at long range, crisp at close range
- 🎤 **Voice Indicator** — Shows voice icon when a player is speaking
- 🔄 **Auto Name Sync** — Server-side caching + periodic sync
- 🛡️ **Disables Native Nametags** — Automatically removes GTA's built-in overhead display
- 🔴 **Damage Flash** — Name turns red for 3 seconds when a player takes damage
- 🐛 **Built-in Debug Command** — `/nametag_debug` for quick troubleshooting

---

## 📦 Installation

### 1. Place the Resource
```
resources/
  └── gtaworld-nametag/
      ├── fxmanifest.lua
      ├── config.lua
      ├── server.lua
      └── client.lua
```

### 2. Add to Server Config
Add the following to `server.cfg` (**must be placed after your framework**):
```cfg
ensure qbx_core           # QBox users
# ensure qb-core          # QBCore users
# ensure es_extended       # ESX users

ensure gtaworld-nametag
```

### 3. Restart the Server

---

## ⚙️ Configuration (`config.lua`)

| Option | Default | Description |
|--------|---------|-------------|
| `Config.Framework` | `'auto'` | `'auto'` / `'esx'` / `'qbcore'` / `'qbox'` |
| `Config.MaxDistance` | `30.0` | Maximum display distance (meters) |
| `Config.FadeStartDistance` | `20.0` | Distance at which fading begins |
| `Config.FontScale` | `0.30` | Font size |
| `Config.DisplayFormat` | `'{name} [{id}]'` | Display format |
| `Config.ShowOwnName` | `false` | Whether to show your own name |
| `Config.RequireLOS` | `true` | Require line of sight to display |
| `Config.ShowVoiceIndicator` | `true` | Show voice activity indicator |
| `Config.DamageColorEnabled` | `true` | Enable red flash on damage |
| `Config.DamageColor` | `{255, 0, 0}` | Color when damaged (RGB) |
| `Config.DamageDuration` | `3000` | Damage color duration (ms) |

### Display Format Examples
```lua
Config.DisplayFormat = '{name} [{id}]'    -- "Jack Perils [1]"
Config.DisplayFormat = '[{id}] {name}'    -- "[1] Jack Perils"
Config.DisplayFormat = 'ID:{id} | {name}' -- "ID:1 | Jack Perils"
```

---

## 🎮 In-Game Commands

| Command | Description |
|---------|-------------|
| `/nametag` | Toggle nametag display on/off |
| `/nametag_debug` | Show debug info (player data status) |

## 🔧 Server Console Commands

Enter the following in txAdmin / server console:
```
nametag_debug
```
Displays framework type and all online player names.

---

## ⚡ Performance Architecture

| Scenario | Cost |
|----------|------|
| Idle (no nearby players) | ~0.00 ms |
| 5 visible players | ~0.01 ms |
| 10 visible players | ~0.02 ms |

---

## ❓ FAQ

**Q: Nothing displays at all?**
1. Type `/nametag_debug` and check if `dataReceived` is `true`
2. Type `nametag_debug` in the server console to verify framework detection
3. Make sure `ensure gtaworld-nametag` comes after your framework in `server.cfg`

**Q: Names don't show under QBox?**
> Manually set `Config.Framework = 'qbox'`

**Q: Showing Steam name instead of character name?**
> The framework may not have fully loaded character data yet. ESX requires the `identity` module.

**Q: How does damage detection work?**
> The scanner thread monitors each player's health every 500ms. When HP decreases, the name turns red for 3 seconds (configurable via `Config.DamageDuration`).

---

## 📄 License
MIT License
