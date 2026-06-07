# 📖 MiniDayZ+ C2Runtime Obfuscation Map
### by [@Civert0](https://t.me/Civert0) — Author/Dev of MDZ ToolkitModMenu v31.0

---

## ⚠️ DISCLAIMER & LEGAL NOTICE

> **I am NOT responsible for how you use this documentation.**
>
> This reference is published strictly for **educational, research, and modding purposes**. By reading and using this material, you accept full responsibility for anything you create with it. Do not use this to harm, exploit, or cheat against other players in any multiplayer context. Use at your own risk.
>
> This documentation is the result of my own independent reverse engineering research on the publicly distributed MiniDayZ+ APK. No proprietary source code is reproduced here — only identifier mappings derived from runtime analysis.

---

## 🧩 What Is This?

This repository contains a **complete obfuscation map** for the **Construct 2 runtime** (`c2runtime.js`) as used in **MiniDayZ+ v1.4–1.9.6+**.

The Construct 2 engine obfuscates all internal identifier names (classes, methods, properties) into short, meaningless symbols like `wa`, `S`, `Fs`, `H`, `W`, etc. This document maps every one of those obfuscated names back to their original, readable Construct 2 equivalents — so you can understand and interact with the game's runtime without needing the unobfuscated source.

---

## 🎯 Purpose

This documentation exists so that **aspiring modders** can:

- Write **external JavaScript mod scripts** for MiniDayZ / MiniDayZ+ without spending months reverse engineering the runtime themselves
- Understand how the **Construct 2 engine internals** work (layouts, layers, instances, types, event sheets, behaviors, etc.)
- Build tools, overlays, trainers, or debug utilities injected via browser console (F12 / Eruda) or a modded WebView
- Learn from my research and **contribute back** to the MiniDayZ modding community

---

## 📁 Files in This Repository

| File | Description |
|------|-------------|
| `C2RUNTIME_OBFUSCATION_MAP_COMPLETE_ENG.txt` | Full obfuscation map — English |
| `C2RUNTIME_OBFUSCATION_MAP_COMPLETE_RU.txt` | Full obfuscation map — Russian (Русский) |
| `README.md` | This file |

---

## Getting Started — How to Use This

### Entry Point
Every external script mod starts here:

```javascript
var rt = window.cr_getC2Runtime();
```

This gives you the full runtime object. From there you can access everything:

```javascript
rt.wa          // currently running layout
rt.wa.ua       // layers array
rt.S           // all object types by index
rt.jg          // all instances by UID (objectsByUid map)
```

### Finding the Player
```javascript
var playerType = rt.S.find(t => t.name === "t181");
var player = playerType.instances[0]; // or playerType.q[0]
console.log(player.x, player.y);
```

### Calling a Game Function
```javascript
c2_callFunction("Spawn_friend_bot");
c2_callFunction("spawn_drop", [itemId, x, y, 1, condition]);
```

### Modifying a Global Variable
```javascript
// Find the global vars array, then find by name
var gVars = /* see map for how to locate this */;
var v = gVars.find(x => x.name === "God_mode");
if (v) v.data = 1;
```

> See **Section 35** of the obfuscation map for a full quick-reference cheat sheet.

---

## 📐 Map Structure

The obfuscation map is organized into parts:

| Part | Contents |
|------|----------|
| A | Global scope — utility functions, class constructors, feature flags |
| B | Core classes — `cr.rect`, `cr.quad`, `cr.CollisionPoly`, `cr.ObjectSet`, etc. |
| C | GLWrap — full WebGL wrapper method map |
| D | Runtime engine — all properties and prototype methods |
| E | Layout & Layer classes |
| F | Type & Instance classes |
| G | Event system — EventSheet, SOL, EventBlock, Condition, Action, Expressions |
| H | Plugin & Behavior system (all 38 constructors) |
| I | Complete objectRefTable (469 entries, indices 0–468) |
| J | Shared ACE methods (common conditions/actions/expressions) |
| K | Shader effects & window globals |
| L | **Quick Reference / Cheat Sheet** ← start here |

---

## 🛠️ Compatible Versions

- **Tested on:** MiniDayZ+ v1.4 → v1.9.6
- **Should work on:** Most MiniDayZ+ versions using the same Construct 2 build
- **May not work on:** Very old versions (pre-1.4) or future versions if the runtime is rebuilt

Scripts can be injected via:
- **Android:** Eruda console embedded in a patched APK, or via a modded WebView
- **Browser (PC):** F12 developer console on the web version
- **Root / ADB:** Direct WebView debugging

Basically you can add custom GUI, custom behaviors, modify ingame behaviors/variables and events without you touching the data.js

..expect bugs/glitches and errors might occur upon changing events and variables..
---

## Contact & Support

- **Telegram:** [t.me/Civert0](https://t.me/Civert0)
- **Ko-fi:** [ko-fi.com/civert0](https://ko-fi.com/civert0)
- **PayPal:** civertzero@gmail.com

If this documentation helped your project, consider dropping a coffee. 😁

for removal or feedback you may contact me at
civertzero@gmail.com 
or [My Telegram](https://t.me/Civert0)

---

## 📜 License

This documentation is shared freely for the MiniDayZ modding community. You may:
- ✅ Use it to build your own mods and tools
- ✅ Share it or idk :P
- ✅ Translate it to other languages

You may NOT:
- ❌ Claim this research as your own
- ❌ Sell this documentation or mods derived from it
- ❌ Use it to develop malware, cheats targeting other players, or any harmful software

---

*MiniDayZ and MiniDayZ+ are properties of their respective owners. This project is unofficial and not affiliated with the game's developers. © 2016-2026 Bohemia Interactive a.s. Mini DAYZ® is a trademark of Bohemia Interactive a.s. All rights reserved*

