<h1 align="center">Hi, I'm Mikhail</h1>
<h3 align="center">AI & Automation Engineer</h3>

---

### About Me

I design and build intelligent systems, AI agents, and bots that automate processes and accelerate product development.

I work at the intersection of architecture, integrations, and LLMs — connecting services, APIs, and data into reliable, scalable workflows. For me, automation is not just scripts, it's a well-thought-out system with clear logic and measurable outcomes.

**Background:** 10 years of sysadmin experience + Android test automation (Kotlin, Kaspresso) — which gave me infrastructure thinking and a systems mindset.

**Currently building:** open source MCP servers that give Claude direct access to home and network infrastructure — treating AI not as a chatbot, but as an agent with real system access.

---

## Open Source Projects

### [ha-filesystem-mcp](https://github.com/st412m/ha-filesystem-mcp)
Home Assistant addon that exposes a local directory to Claude via MCP (Model Context Protocol). Built to implement [Andrej Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — a personal knowledge base in plain markdown files, maintained by an LLM agent.

- Exposes any local directory (e.g. USB drive) via MCP over HTTPS
- Token-based auth compatible with claude.ai custom connectors
- Auto-creates vault structure and `CLAUDE.md` on first run
- Works together with HA-MCP and Keenetic-MCP for full smart home context
- Tested on amd64 · [Community thread](https://community.home-assistant.io/t/filesystem-mcp-server-expose-your-local-directory-to-claude-karpathy-llm-wiki-for-home-assistant/)

### [keenetic-mcp](https://github.com/st412m/keenetic-mcp)
MCP server for Keenetic routers. Runs directly on the router via Entware, allowing Claude to monitor and manage home network infrastructure.

- 23 tools: system monitoring, WiFi analysis, client management, VPN status, Mesh topology, backup scheduler
- Pure Python, no external dependencies
- Tested on Keenetic Giga KN-1010, KeeneticOS 5.0.11

### [nowinandroid](https://github.com/st412m/nowinandroid)
Custom UI test automation framework built on top of Google's Now in Android app. DSL-based approach with Kaspresso, full Jetpack Compose support, and Allure reporting integration.

---

## Technologies

- **AI & Agents**: Claude (Anthropic), Model Context Protocol, n8n
- **Home Automation**: Home Assistant, Zigbee2MQTT, LocalTuya, Keenetic
- **Languages**: Python, JavaScript, Kotlin
- **Infrastructure**: Linux, Docker, VPS, self-hosted
- **Android QA**: Kaspresso, Espresso, UI Automator, Allure

---

### Contact

- [LinkedIn — Mikhail Staroverov](https://www.linkedin.com/in/mikhail-staroverov/)

---

> *If a process can be automated — it should be. If it can't — prepare it, then automate it.*



