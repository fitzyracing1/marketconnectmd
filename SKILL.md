---
name: marketconnect
description: Activate for the Market Connect project (fitzyracing1/marketconnect) — Base44 idea submission and market connection platform. Use for development, debugging, feature work, Base44 entities, GitHub Pages, or when discussing idea submissions, status tracking (pending/approved/rejected), or the Barrage plain-language explanation of the app. Triggers include marketconnect, market connect, idea submission platform, base44 marketconnect, fitzyracing1/marketconnect.
---

# Market Connect

Specialized instructions for the Market Connect Base44 app repository (https://github.com/fitzyracing1/marketconnect).

## Project Context

Treat this as user-owned application code. Keep changes focused on the request and preserve existing project conventions.

Start with `README.md` for local setup, environment variables, and publish workflow.

This is a clone of `market-connect` published as `marketconnect` for cleaner naming and GitHub Pages hosting.

Live demo (when Pages enabled): https://fitzyracing1.github.io/marketconnect/

## Base44 References

- CLI overview: https://docs.base44.com/developers/references/cli/get-started/overview.md
- Agent skills: https://docs.base44.com/developers/backend/overview/skills.md

If the agent supports Agent Skills, install or update Base44 skills before Base44-specific work:

```bash
npx skills add base44/skills
```

## Key Files

- `src/` — React + Vite frontend
- `src/api/base44Client.js` — frontend Base44 SDK client
- `vite.config.js` — Vite config and Base44 Vite plugin setup
- `base44/` — Entity schemas and app config (`config.jsonc`, `entities/`)
- `.env.local` — local-only environment values; never commit secrets
- `src/pages/` — Main routes (Home, Login, Dashboard, SubmissionDetail, etc.)
- `src/components/` — UI and feature components

## Development Workflow

- Use `base44 dev` as the default local development command when you need the local Base44 backend. It can run the backend and frontend together.
- When docs or code mention the frontend being started automatically, that usually means the Base44 project config includes `site.serveCommand`, for example `"serveCommand": "npm run dev"` in `base44/config.jsonc`.
- Use `npm run dev` only for frontend-only work against the hosted Base44 backend.
- Prefer the existing Base44 CLI workflow over adding new npm scripts for Base44-specific tasks.
- Reuse the existing SDK client and Vite plugin patterns before adding new Base44 integration paths.
- Run the relevant checks from `package.json` before finishing code changes.

## Core Entities

Primary entity: `IdeaSubmission`

Required fields: title, description, submittedBy

Key fields: category, status (enum: pending, approved, rejected, in_review), contactEmail, attachments, createdAt, updatedAt

User entity also present.

## Barrage Plain-Language Description

When explaining the project to non-programmers or packaging descriptions, use or expand this Barrage form:

```
# Market Connect

> A simple online place where people can submit their ideas and others can see and connect with them.

## Purpose
Market Connect lets anyone type out a new idea, save it, and share it. Other people can look at the ideas, leave feedback, or decide they want to work with the person who submitted it. It is built so that the website and the behind-the-scenes data storage talk to each other cleanly.

## How it works (plain English)
1. A visitor opens the website.
2. They can create an account or sign in.
3. Once signed in, they can write a short description of their idea and submit it.
4. The idea is stored and appears on a list that other signed-in users can browse.
5. Anyone can open a single idea to see more details.
6. The system keeps track of who submitted what and whether the idea is still waiting, approved, or rejected.

## Key ideas
- Account system (sign up / sign in so we know who is talking)
- Idea submission form (a simple box where you type your idea)
- Idea list and detail pages (so people can browse and open individual ideas)
- Status tracking (pending, approved, rejected)

## The actual code structure
The project is organized into folders:
- pages → the different screens people see (home, login, dashboard, idea details)
- components → reusable pieces such as the navigation bar and buttons
- lib → helper code that handles user accounts and common tools
- api → the connection to the Base44 backend that stores the data

## Decisions the program makes
- If you are not signed in, you are sent to the login page when you try to open the dashboard.
- After you submit an idea, it starts with the status “pending”.
- The home page shows different buttons depending on whether you are already signed in or not.
```

## GitHub Pages

1. Go to the repository Settings → Pages
2. Under Build and deployment, set Source to GitHub Actions
3. The included workflow (`.github/workflows/deploy-pages.yml`) will automatically build and deploy on every push to `main`

## License

Private / proprietary to the project owner.

## Working Rules

- Preserve the existing Base44 entity schemas and auth patterns unless the user explicitly requests changes.
- Prefer minimal, focused diffs that match the current React + Vite + Base44 style.
- When adding features, keep the Barrage-style plain-English explanations up to date in README if the core behavior changes.
- Never commit secrets. Keep all environment values in `.env.local`.
