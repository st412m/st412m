<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">AI & Automation Engineer</h3>

---

### About Me

I design and build intelligent systems, AI agents, and bots that automate processes and accelerate product development.

I work at the intersection of architecture, integrations, and LLMs — connecting services, APIs, and data into reliable, scalable workflows. For me, automation is not just scripts, it's a well-thought-out system with clear logic and measurable outcomes.

**Background:** 10 years of sysadmin experience + Android test automation (Kotlin, Kaspresso) — which gave me infrastructure thinking and a systems mindset.

**Currently building:** a family of open source MCP servers that give Claude direct, authenticated access to real infrastructure — files, router, Android devices — treating AI not as a chatbot, but as an agent with system access and the guard rails that requires.

They are designed to work together: the router server knows the network, the Android server operates the devices on it, and the filesystem server holds the notes tying both together. Each one is useful on its own.

---

## Open Source Projects

### [ha-adb-mcp](https://github.com/st412m/ha-adb-mcp) · v1.0.0
Home Assistant addon exposing **network ADB** over MCP, so an assistant can actually operate Android TVs, Fire TVs, phones and tablets on the LAN — not just read their state.

- 16 tools: shell, screenshots, UI dump with tap coordinates, input, app install/uninstall, file transfer, logcat
- Split-APK support via `install-multiple` — restoring an app after a factory reset is one call
- Unicode input (Cyrillic/emoji/CJK) through ADBKeyBoard, with automatic IME switch and restore
- Coexists with the HA `androidtv` integration by sharing one adb server instead of fighting over the device session
- Logcat filtering runs on-device, so large buffers never cross the wire
- amd64 · aarch64 build-verified on RPi 4

### [keenetic-mcp](https://github.com/st412m/keenetic-mcp) · v2.5.0
MCP server for Keenetic routers. Runs directly on the router via Entware, letting Claude monitor and manage home network infrastructure.

- 42 tools: system and traffic monitoring, WiFi analysis, client management, VPN and mesh topology, extender logs, firewall and port-forwarding rules, backup scheduler
- Write tools default to `dry_run: true`, save the config after every change, and verify by re-reading the affected branch — the answer is a before/after diff, not a "command sent" claim
- Guard rails in code: the server can never close the channel it is reached through; anything else you want shielded is configurable
- Pure Python, standard library only — no dependencies to install on a router
- Tested on Keenetic Giga KN-1010 + KN-1011 (Mesh), KeeneticOS 5.1.1

### [ha-filesystem-mcp](https://github.com/st412m/ha-filesystem-mcp) · v2.4.1
Home Assistant addon that exposes a local directory to Claude via MCP. Built to implement [Andrej Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — a personal knowledge base in plain markdown, maintained by an LLM agent.

- Exposes any local directory (e.g. a USB drive) via MCP over HTTPS
- Token-based auth compatible with claude.ai custom connectors
- Auto-creates the vault structure and `CLAUDE.md` on first run
- amd64 · aarch64

### [nowinandroid](https://github.com/st412m/nowinandroid)
Custom UI test automation framework built on top of Google's Now in Android app. DSL-based approach with Kaspresso, full Jetpack Compose support, and Allure reporting integration.

---

## Technologies

- **AI & Agents**: Claude (Anthropic), Model Context Protocol, n8n
- **Home Automation**: Home Assistant, Zigbee2MQTT, LocalTuya, Keenetic
- **Languages**: Python, JavaScript, Kotlin
- **Infrastructure**: Linux, Docker, VPS, self-hosted
- **Android**: ADB, Kaspresso, Espresso, UI Automator, Allure

---

### Contact

- [LinkedIn — Mikhail Staroverov](https://www.linkedin.com/in/mikhail-staroverov/)

---

> *If a process can be automated — it should be. If it can't — prepare it, then automate it.*
