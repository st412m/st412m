<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">AI & Automation Engineer</h3>

---

### About Me

I build systems where AI does the work rather than talks about it: connecting models to real infrastructure — files, networks, devices — and making sure they have brakes.

Before that: 10 years of system administration and Android test automation (Kotlin, Kaspresso).

---

## Open Source Projects

MCP servers that give an assistant a way into real infrastructure: the network, the devices on it, files and documents. Each is useful on its own. Together they make one system: the assistant sees what is going on, can change it, keeps notes on what it did, and hands bulk reading to cheap models instead of spending its own working memory on it. Documents are turned into text for them by a shared library, doclines, so any line can be quoted and checked.

They are all built on one principle. An agent with system access will sooner or later be asked to do something destructive, so these servers are made to refuse rather than to trust. A call that changes something shows a plan first. What must not be touched is read from the live system, not hardcoded. Success is reported only after the result has been read back. And nothing a helper model says is taken on faith.

### [cheap-eyes](https://github.com/st412m/cheap-eyes)

Reading big text is expensive for an assistant like Claude: a megabyte of log or a hundred-page contract eats its working memory when it needs a dozen lines from it. cheap-eyes hands that reading to a cheap model and gives the assistant back only what it asked for, with the exact place in the source.

The cheap model is not taken at its word. The server checks every quote and every line reference against the original and flags anything that isn't there. That catches what was made up, not what was missed, and the docs say so plainly.

It reads plain text and logs, PDF, Word, PowerPoint, OpenDocument, EPUB, FB2, EML and MSG mail with attachments, and web pages by link. An answer shows where a line came from: page, slide, chapter or mail attachment. Give it your own form as JSON, say the deadline, price and bid security from a tender pack, and it comes back filled in, with a quote for every value. Search by an exact pattern runs without a model at all and costs nothing. Spreadsheets are left out on purpose: exact questions about a table are better answered by grep or code.

The model sees only numbered lines with secrets already masked, and has no tools. Only Zero Data Retention providers are used. Runs from npx, in Docker or as a Home Assistant add-on, and is listed in the official MCP Registry.

### [doclines](https://github.com/st412m/doclines)

A Node.js library that turns a document into numbered lines of text and marks where each page, slide, chapter, sheet or mail attachment begins. A reference like "line 812, page 4 of the attachment" can then be checked mechanically; cheap-eyes' quote check rests on that.

It reads PDF, Word (old DOC included), RTF, HTML, Excel (old XLS included), PowerPoint, OpenDocument, EPUB, FB2, and EML and MSG mail with attachments. The format is told by content, not by file extension. Encrypted files, scans with no text layer, images and archives are refused with a reason.

Each document is parsed in a separate thread with a time and memory limit, so a broken or hostile file can't take down the program reading it. Comes with a `doclines <file>` command.

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

- **AI & Agents**: Claude (Anthropic), OpenRouter, Model Context Protocol, n8n
- **Home Automation**: Home Assistant, Zigbee2MQTT, LocalTuya, Keenetic
- **Languages**: Python, JavaScript, Kotlin
- **Infrastructure**: Linux, Docker, VPS, self-hosted
- **Android**: ADB, Kaspresso, Espresso, UI Automator, Allure

---

### Contact

- [LinkedIn — Mikhail Staroverov](https://www.linkedin.com/in/mikhail-staroverov/)

---

> *If a process can be automated — it should be. If it can't — prepare it, then automate it.*

