---
name: auto-deploy
description: Auto-detect project type and deploy to the best-fit platform with zero-config. Use when the user says deploy, publish, launch, go live, or wants to put a project online.
---

# Auto Deploy

One-shot deployment: detect the project, pick the right platform, configure, and deploy.

## Detection

1. Read root directory and config files
2. Classify from signals:

| Signal | Type | Platform |
|---|---|---|
| next.config.* | Next.js | Vercel |
| astro.config.* | Astro | Vercel |
| remix.config.* | Remix | Vercel |
| vite.config.* | SPA | Vercel |
| svelte.config.* | SvelteKit | Vercel |
| nuxt.config.* | Nuxt | Vercel |
| react-scripts | CRA | Netlify |
| requirements.txt + fastapi | FastAPI | Render |
| requirements.txt + flask | Flask | Render |
| requirements.txt + django | Django | Render |
| package.json + express | Express | Render |
| go.mod | Go | Render |
| Cargo.toml | Rust | Render |
| index.html only | Static | Netlify |
| wrangler.toml | Worker | Cloudflare |

If frontend+backend both exist, ask user which to deploy.

## Platform Selection

- Frontend: Vercel (default) or Netlify
- Static: Netlify or Cloudflare Pages
- Backend: Render
- Edge: Cloudflare
- Full-stack: Vercel + Render separately

Install platform skill first if missing.

## Deployment

**Vercel:** Load vercel-deploy, generate vercel.json if missing, deploy, report URL.

**Netlify:** Load netlify-deploy, generate netlify.toml if needed, deploy, report URL.

**Render:** Load render-deploy, generate render.yaml, deploy, report deeplink.

**Cloudflare:** Load cloudflare-deploy, check wrangler.toml, deploy, report URL.

## Post-Deploy

- Print live URL
- Offer browser test
- Offer deployment badge if README exists
