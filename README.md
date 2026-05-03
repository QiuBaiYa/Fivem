# 🎮 GTA World 同款姓名显示插件 v1.0.0

> FiveM 高性能头顶姓名显示插件，同时支持 **ESX** / **QBCore** / **QBox** 三大框架

---

## ✨ 功能特点

- 🎯 **GTA World 同款风格** — 玩家头顶显示 `角色姓名 (ID)` 格式
- 🔧 **三框架支持** — 自动检测 ESX / QBCore / QBox (qbx_core)
- ⚡ **极致性能优化** — 双线程架构，不会造成任何卡顿
- 📏 **距离渐变透明** — 远距离自动淡出，近距离清晰显示
- 🎤 **语音指示器** — 说话时显示语音标识
- 🔄 **自动名称同步** — 服务端缓存 + 定时同步
- 🛡️ **禁用原生名牌** — 自动关闭 GTA 自带的头顶显示
- 🐛 **内置调试命令** — `/nametag_debug` 快速排查问题

---

## 📦 安装步骤

### 1. 放置资源
```
resources/
  └── gtaworld-nametag/
      ├── fxmanifest.lua
      ├── config.lua
      ├── server.lua
      └── client.lua
```

### 2. 添加启动项
在 `server.cfg` 中添加（**确保在框架之后**）：
```cfg
ensure qbx_core           # QBox 用户
# ensure qb-core          # QBCore 用户
# ensure es_extended       # ESX 用户

ensure gtaworld-nametag
```

### 3. 重启服务器

---

## ⚙️ 配置说明 (`config.lua`)

| 配置项 | 默认值 | 说明 |
|--------|--------|------|
| `Config.Framework` | `'auto'` | `'auto'` / `'esx'` / `'qbcore'` / `'qbox'` |
| `Config.MaxDistance` | `30.0` | 最大显示距离（米） |
| `Config.FadeStartDistance` | `20.0` | 开始淡出的距离 |
| `Config.FontScale` | `0.30` | 字体大小 |
| `Config.DisplayFormat` | `'{name} ({id})'` | 显示格式 |
| `Config.ShowOwnName` | `false` | 是否显示自己的名字 |
| `Config.RequireLOS` | `true` | 是否需要视线可见 |
| `Config.ShowVoiceIndicator` | `true` | 是否显示语音指示器 |

### 显示格式示例
```lua
Config.DisplayFormat = '{name} ({id})'    -- "JackPerils [1]"
Config.DisplayFormat = '[{id}] {name}'    -- "[1] JackPerils"
Config.DisplayFormat = 'ID:{id} | {name}' -- "ID:1 | JackPerils"
```

---

## 🎮 游戏内命令

| 命令 | 说明 |
|------|------|
| `/nametag` | 切换姓名显示开关 |
| `/nametag_debug` | 显示调试信息（玩家数据状态） |

## 🔧 服务端调试命令

在 txAdmin / 服务器控制台输入：
```
nametag_debug
```
可查看框架类型和所有在线玩家姓名。

---

## ⚡ 性能优化架构


| 场景 | 耗时 |
|------|------|
| 空闲（附近无人） | ~0.00 ms |
| 5 个可见玩家 | ~0.01 ms |
| 10 个可见玩家 | ~0.02 ms |

---

## ❓ 常见问题

**Q: 完全不显示？**
1. 输入 `/nametag_debug` 查看 `dataReceived` 是否为 `true`
2. 服务端控制台输入 `nametag_debug` 查看框架检测结果
3. 确认 `server.cfg` 中 `ensure gtaworld-nametag` 在框架之后

**Q: QBox 下不显示角色名？**
> 手动设置 `Config.Framework = 'qbox'`

**Q: 显示 Steam 名而不是角色名？**
> 框架可能未完全加载角色数据。ESX 需要 identity 模块。

---

## 📄 License
MIT License
