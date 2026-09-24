# AGENTS.md

Read by every coding agent (Claude Code, Codex, Cursor, etc.) in repos created from this template.
`CLAUDE.md` contains `@AGENTS.md` plus anything Claude-specific.
Rationale for rules lives in [ADRs](docs/adr/README.md).

**Stacks below are defaults, not suggestions.** Use them unless Section 1 overrides. Anything outside this list → stop, ask, explain why in 1–2 sentences.

**Be extremely concise** in replies, commits, and docs. Sacrifice grammar for concision.

---

## 1. Project context (fill in per project)

<!-- /new-project skill fills this. Keep under ~30 lines. Delete unused rows. -->

- **Name:**
- **One-line pitch:**
- **Type:** web app | marketing site | mobile app | API/service | Python/data | launch assets
- **Audience:**
- **Brand:** primary colour, accent, font(s), tone
- **Deploy target:**
- **Overrides to defaults:**

### Architecture overview
<!-- 3–8 lines: main modules, data flow, where entry points live. -->

### Task routing
| Task | Key rules | ADRs |
|------|-----------|------|
| <!-- e.g. add API endpoint --> | <!-- §2d, §4 --> | <!-- ADR-003 --> |

---

## 2. Default stacks by project type

### 2a. Web app / SaaS dashboard
| Concern | Default | Docs |
|---|---|---|
| Framework | Next.js (App Router) + TypeScript | https://nextjs.org |
| Styling | Tailwind CSS | https://tailwindcss.com |
| Components | shadcn/ui (Radix underneath) | https://ui.shadcn.com |
| Icons | Lucide | https://lucide.dev |
| Animation | Motion | https://motion.dev |
| Charts | Recharts (via shadcn charts) | https://ui.shadcn.com/charts |
| Forms / validation | React Hook Form + Zod | https://zod.dev |
| DB / ORM | Postgres + Drizzle | https://orm.drizzle.team |
| Auth | Better Auth | https://www.better-auth.com |
| Tests | Vitest (unit), Playwright (e2e + screenshots) | https://playwright.dev |

### 2b. Marketing / landing website
Same base as 2a, plus:
| Concern | Default | Docs |
|---|---|---|
| Animated sections | Magic UI (MIT) | https://magicui.design |
| Scroll / timeline animation | GSAP + ScrollTrigger | https://gsap.com |
| 3D hero / product visuals | Three.js via React Three Fiber + drei | https://r3f.docs.pmnd.rs |
| Lottie | dotLottie | https://lottiefiles.com |
| Content | MDX | https://mdxjs.com |

One hero effect per page. Respect `prefers-reduced-motion` (static render when set — an accessibility requirement, not a code fallback).

### 2c. Mobile app
| Concern | Default | Docs |
|---|---|---|
| Framework | Expo + Expo Router + TypeScript | https://expo.dev |
| Styling | NativeWind | https://www.nativewind.dev |
| Components | React Native Reusables | https://reactnativereusables.com |
| Animation | Reanimated + Gesture Handler | https://docs.swmansion.com/react-native-reanimated |
| Icons | lucide-react-native | https://lucide.dev |
| State / data | TanStack Query + Zustand | https://tanstack.com/query |

### 2d. API / backend service (TypeScript)
| Concern | Default | Docs |
|---|---|---|
| Framework | Hono | https://hono.dev |
| Validation | Zod | https://zod.dev |
| DB / ORM | Postgres + Drizzle | https://orm.drizzle.team |
| Infra | AWS via CDK (see AWS MCP) | https://github.com/awslabs/mcp |
| Tests | Vitest | https://vitest.dev |

### 2e. Python / data / scripts
| Concern | Default | Docs |
|---|---|---|
| Env + deps | uv (never pip / `python -m venv`) | https://docs.astral.sh/uv |
| Dataframes | Polars (never Pandas) | https://pola.rs |
| Charts | Altair (not matplotlib) | https://altair-viz.github.io |
| Paths | `pathlib` (not `os.path`) | — |
| Tests | pytest, plain functions (`def test_foo(tmp_path):`, no classes) | https://docs.pytest.org |

uv usage:
```bash
uv venv && uv sync      # setup (idempotent, safe to rerun)
uv run pytest           # tests
uv run example.py       # run script, no activation needed
make install|run|test   # prefer Makefile targets when present
```
Conventions: deps in `pyproject.toml`; `uv.lock` committed; `.venv/` and `data/` gitignored.

### 2f. Launch assets (videos, social clips, OG images)
| Concern | Default | Docs |
|---|---|---|
| Promo video (React) | Remotion + official skills | https://www.remotion.dev/docs/ai/skills |
| Promo video (HTML/GSAP, fully OSS) | HyperFrames | https://github.com/heygen-com/hyperframes |
| OG / social images | Satori / `next/og` | https://github.com/vercel/satori |
| Real-app screen recordings | Playwright video capture | https://playwright.dev/docs/videos |

Remotion needs a paid company license above small team size — check https://www.remotion.dev/license. Default to HyperFrames if licensing unclear.
Reuse brand tokens from §1 and the app's Tailwind theme. Render → inspect frames → fix → re-render before done.

---

## 3. Skills and plugins

Install via `npx skills` (https://skills.sh) or the Claude Code plugin marketplace.

| When | Skill / plugin | Install |
|---|---|---|
| Every project, before building | grill-me | `npx skills@latest add mattpocock/skills --skill=grill-me` |
| Editing agent docs | writing-for-agents | `npx skills@latest add mattpocock/skills --skill=writing-for-agents` |
| Any UI | Anthropic frontend-design | https://github.com/anthropics/skills |
| Any UI | Playwright MCP | https://github.com/microsoft/playwright-mcp |
| Launch video | Remotion skills | `npx remotion skills add` |
| Launch video | HyperFrames skills | `npx skills add heygen-com/hyperframes` |
| AWS infra | AWS MCP servers | https://github.com/awslabs/mcp |

---

## 4. Core principles

Design
1. Don't overengineer — simple beats complex.
2. No fallbacks — one correct path, no alternatives.
3. One way — one way to do each thing.
4. Clarity over compatibility — clear code beats backward compatibility.
5. Throw errors — fail fast when preconditions aren't met.
6. No backups — trust the primary mechanism.
7. Separation of concerns — one responsibility per function.

Methodology
8. Surgical changes only — minimal, focused diffs.
9. Evidence-based debugging — minimal, targeted logging.
10. Fix root causes, not symptoms.
11. Collaborate — work with the user to find the most efficient solution.

---

## 5. Working rules

| Need | Answer |
|------|--------|
| Validate changes | `ci/validate` — mandatory, never skip |
| Run tests | `ci/test` |

1. **Look at what you build.** UI changes: run app, Playwright screenshots at 390px + 1440px, review before reporting done.
2. **Design tokens first.** Colours, radius, fonts, spacing in Tailwind theme / CSS vars. No hard-coded hex in components.
3. **No new deps outside §2 without asking.**
4. **Accessibility baseline:** semantic HTML, keyboard reachable, visible focus, AA contrast.
5. **Record decisions.** Non-obvious choices → `docs/adr/NNN-title.md` (3–10 lines). Link from §1 task routing.

<!-- Add per-project rules here only when they exist. Don't keep empty headings. Topics to consider: performance, determinism, error handling, code style, testing, dependencies. -->

---

## 6. Keeping this file up to date

When user says "update the stack", "switching to X", or a project proves a default wrong:
1. Propose edit as a diff — never apply silently.
2. Each default: name, reason if non-obvious, docs link.
3. Replace old option, don't stack both, unless each has a clear "use when".
4. Add changelog line.
5. Keep under ~200 lines. Overflow → `docs/stack/<topic>.md` + one-line pointer here.

### Stack changelog
- 2026-09-24 — Initial version; merged Python/uv rules and core principles from previous agent.md.
