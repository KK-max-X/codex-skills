# Codex Skills Marketplace

AI-powered skills for Codex ? one-click install, instant productivity boost.

---

## ?? spawn-orchestrator ? Multi-Agent Parallel Executor

**Turn complex projects into parallel workers.**

When you have a large task, spawn-orchestrator automatically splits it into independent sub-tasks and spawns parallel agents to execute them simultaneously. Think of it as a "manager AI" that delegates work to "worker AIs."

- Auto-decompose complex tasks into parallel units
- Conflict-free write scopes across agents
- Automatic result assembly and integration
- **Cut multi-hour projects to minutes**

[View skill](skills/spawn-orchestrator/SKILL.md)

```bash
python install-skill-from-github.py --repo KK-max-X/codex-skills --path skills/spawn-orchestrator
```

---

## ?? auto-deploy ? One-Click Universal Deploy

**Zero config. Deploy anything. 15+ frameworks.**

Drop a project link, auto-deploy reads your codebase, detects the framework, picks the best platform, and deploys it. No more wrestling with build configs and deployment scripts.

- Supports React, Vue, Next.js, Nuxt, Astro, SvelteKit, Flask, Django, FastAPI, Express, Go, Rust, and more
- Auto-selects Vercel / Netlify / Render / Cloudflare
- Generates missing config files automatically
- **From repo to live URL in under 2 minutes**

[View skill](skills/auto-deploy/SKILL.md)

```bash
python install-skill-from-github.py --repo KK-max-X/codex-skills --path skills/auto-deploy
```

---

## ?? ai-code-review ? Automated PR Review with Severity Ratings

**Your AI code reviewer that never sleeps.**

Drop a GitHub PR link, and ai-code-review reads every changed file, identifies bugs, security vulnerabilities, and code smells, then attaches inline comments with P0/P1/P2 severity ratings.

- **P0 Critical**: Security holes, data loss risks, crash-causing bugs
- **P1 High**: Logic errors, performance bottlenecks, missing error handling
- **P2 Medium**: Code quality, naming, missing tests
- Covers Python, JavaScript/TypeScript, Go, Rust, Java, SQL
- **Merge with confidence**

[View skill](skills/ai-code-review/SKILL.md)

```bash
python install-skill-from-github.py --repo KK-max-X/codex-skills --path skills/ai-code-review
```

---

## Installation

Each skill installs with one command:

```bash
python install-skill-from-github.py --repo KK-max-X/codex-skills --path skills/<skill-name>
```

Requires Codex desktop app with the skill-installer skill enabled.

## Custom Skills

Need a custom skill for your team or project? Contact: [GitHub Issues](https://github.com/KK-max-X/codex-skills/issues)

---

## License

Free for personal use. Commercial use requires a license — contact via [GitHub Issues](https://github.com/KK-max-X/codex-skills/issues).
