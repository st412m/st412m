<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">AI & Automation Engineer</h3>

---

### About Me

I build systems where AI does the work rather than talks about it: connecting models to real infrastructure — files, networks, devices — and making sure they have brakes.

Before that: 10 years of system administration and Android test automation (Kotlin, Kaspresso).

---

## Open Source Projects

Three MCP servers. Each is useful on its own; together they give an assistant a way into a home setup — the router server knows the network, the ADB server operates the devices on it, and the filesystem server holds the notes that tie the two together.

One principle runs through all three: an agent with system access will eventually be asked to do something destructive, so these servers are built to refuse rather than to trust. Calls that change state show a plan instead of acting, protected lists are derived from the live system rather than hardcoded, and nothing reports success before reading back what it did.

### [keenetic-mcp](https://github.com/st412m/keenetic-mcp)

An MCP server for Keenetic routers. It runs on the router itself through Entware, in plain Python with no dependencies.

The assistant sees the network — clients, traffic, Wi-Fi and interference, VPN, mesh, firewall rules and port forwards — and can change it, with a preview first and a re-read afterwards. There is a plain HTTP route for clients that don't speak MCP, and a background watcher that calls out on its own when something happens on the router: a webhook, ntfy, the Telegram Bot API, whatever the rule names.

Tested on a Keenetic Giga KN-1010 + KN-1011 (Mesh), KeeneticOS 5.1.

### [ha-adb-mcp](https://github.com/st412m/ha-adb-mcp)

A Home Assistant add-on that exposes network ADB over MCP, so an assistant can operate the Android TVs, streaming boxes, phones and watches on the LAN instead of only reading their state.

Shell, screenshots with coordinates that actually land, text input including Unicode, app installs from bundles, file transfer, logcat. Package operations get their own guard rails: the protected set is derived from the device itself — launcher, active IME, package installer, role holders, packages holding a listening socket — any overlap aborts the whole call, and everything applied is written to a snapshot that one call undoes.

Every release is accepted on live hardware across five device classes: Fire OS, Android TV, Google TV, Android 16 and Wear OS.

### [ha-filesystem-mcp](https://github.com/st412m/ha-filesystem-mcp)

A Home Assistant add-on that opens a local directory to an assistant — a USB drive on the server, for instance.

Built for [Andrej Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f): a personal knowledge base in plain markdown, maintained by the agent itself. It reads PDFs as text, so scanned manuals land in the same wiki as everything else, and reads SQLite databases read-only.

### [nowinandroid](https://github.com/st412m/nowinandroid)

A UI test automation framework built on Google's Now in Android app: a DSL on top of Kaspresso, full Jetpack Compose support, Allure reporting.

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

