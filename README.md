<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">AI & Automation Engineer</h3>

---

### About Me

I design and build intelligent systems, AI agents, and bots that automate processes and accelerate product development.

I work at the intersection of architecture, integrations, and LLMs — connecting services, APIs, and data into reliable, scalable workflows. For me, automation is not just scripts, it's a well-thought-out system with clear logic and measurable outcomes.

**Background:** 10 years of sysadmin experience + Android test automation (Kotlin, Kaspresso) — which gave me infrastructure thinking and a systems mindset.

**Currently building:** a family of open source MCP servers that give Claude direct, authenticated access to real infrastructure — files, router, Android devices — treating AI not as a chatbot, but as an agent with system access and the guard rails that requires.

They are designed to work together: the router server knows the network, the Android server operates the devices on it, and the filesystem server holds the notes tying both together. Each one is useful on its own.

The guard rails are the interesting part. An agent with system access will eventually be asked to do something destructive, so the servers are built to refuse rather than to trust: state-changing calls preview by default, protected sets are derived from the live system instead of hardcoded, and nothing reports success it has not read back and verified.

The router server now also works in the other direction: it watches the router from the inside and calls out when something happens, so an event no longer has to wait for someone to ask about it.

---

## Open Source Projects

### [keenetic-mcp](https://github.com/st412m/keenetic-mcp) · v2.7.4
MCP server for Keenetic routers. Runs directly on the router via Entware, letting Claude monitor and manage home network infrastructure.

- 47 tools: system and traffic monitoring, WiFi analysis, client management, VPN and mesh topology, extender logs, firewall and port-forwarding rules, backup scheduler
- Write tools default to `dry_run: true`, save the config after every change, and verify by re-reading the affected branch — the answer is a before/after diff, not a "command sent" claim
- Guard rails in code: the server can never close the channel it is reached through; anything else you want shielded is configurable
- **Plain HTTP route** alongside MCP, for clients that don't speak the protocol (Home Assistant `rest_command`, curl, shell scripts). Read-only by default — tools that change state are refused unless named explicitly
- **Event watcher**: a background thread polls the router locally — log lines by regex, or a diff over any RCI branch — and makes an outbound HTTP call when a rule matches. Rules are one JSON file, re-read on change without a restart. Nothing in the code knows about Home Assistant: a rule carries its own method, URL, headers and body, so a webhook, ntfy and the Telegram Bot API are all equally first-class
- The watcher keeps its own RCI session rather than sharing the server's. It didn't at first, and a ten-second poll of a six-second `show log` meant every other call could wait that long — measured, then fixed
- State lives in RAM, never on the router's USB flash. A reboot re-baselines instead of replaying a boot's worth of log lines as alerts
- Pure Python, standard library only — no dependencies to install on a router
- Tested on Keenetic Giga KN-1010 + KN-1011 (Mesh), KeeneticOS 5.1.1

### [ha-adb-mcp](https://github.com/st412m/ha-adb-mcp) · v1.3.0
Home Assistant addon exposing **network ADB** over MCP, so an assistant can actually operate Android TVs, Fire TVs, phones, tablets and watches on the LAN — not just read their state.

- 18 tools: shell, screenshots, UI dump with tap coordinates, input, app install/uninstall, file transfer, logcat, plus package operations and element activation below
- **Package operations with guard rails.** Bulk package work is where an assistant can do real damage, so `adb_app` assumes it will eventually be asked to do something wrong. Everything that changes state defaults to `dry_run: true`. The protected set is **derived from the device** — current launcher, active IME, package installer, WebView provider, role holders, account authenticators, packages holding a listening socket — and any overlap aborts the whole call, with no override flag. An account canary runs between batches, because losing a device's registration is a failure you only notice later, at the store. Everything applied is written to a snapshot, so one call undoes it
- **App bundles.** `.apks` / `.xapk` / `.apkm` install directly: splits are chosen from the device's real ABI list, density and locale, then installed with `install-multiple`. Unpacking happens addon-side, so it works on devices with no `unzip` — Fire OS 7 among them. A missing ABI split is refused, since a wrong ABI leaves an app that will not start; a density miss falls back to the nearest bucket and says so
- **Find an element and activate it in one call.** How it activates is derived, not assumed: with a real touchscreen the element centre is tapped; on a leanback TV device — where a coordinate tap silently activates whatever has focus instead — the focus is walked there with DPAD keys first. The UI is re-dumped after every key, and if the focus stalls, cycles, or runs out of budget, the tool reports the path it walked and presses nothing
- Nothing reports success it has not verified: a launch is confirmed against the resumed activity, an install against the resulting split set, a removal against a re-read of the device
- Unicode input (Cyrillic/emoji/CJK) through ADBKeyBoard, with automatic IME switch and restore
- Coexists with the HA `androidtv` integration by sharing one adb server instead of fighting over the device session
- Logcat filtering runs on-device, so large buffers never cross the wire
- Every release is accepted on live hardware across five device classes — Fire OS 7, Android TV, Google TV, Android 16 and Wear OS 6 — which is where most of these fixes came from: each new class exposed a defect the others could not
- amd64 · aarch64 build-verified on RPi 4

### [ha-filesystem-mcp](https://github.com/st412m/ha-filesystem-mcp) · v2.7.2
Home Assistant addon that exposes a local directory to Claude via MCP. Built to implement [Andrej Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — a personal knowledge base in plain markdown, maintained by an LLM agent.

- Exposes any local directory (e.g. a USB drive) via MCP over HTTPS
- Token-based auth compatible with claude.ai custom connectors
- Auto-creates the vault structure and `CLAUDE.md` on first run
- Reads PDFs as text, so scanned manuals and datasheets land in the same wiki as everything else
- amd64 · aarch64, community-confirmed on a Raspberry Pi 4

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
