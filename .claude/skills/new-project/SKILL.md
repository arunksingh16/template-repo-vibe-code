---
name: new-project
description: Bootstrap a new repo created from this template. Use when the user says "new project", "set up this repo", "prepare repo", or runs /new-project.
---

# New project bootstrap

Work through these steps in order. Ask the user only for what you cannot infer from the repo or conversation.

1. **Understand the project.** Ask for (or read) a one-line pitch, the project type (web app, marketing site, mobile app, API/service, Python/data, launch assets), audience, and brand basics (colours, fonts, tone). If the idea is still vague, suggest running /grill-me first.
2. **Fill in Section 1 of AGENTS.md** (context, architecture overview, task routing). Delete unused rows. Create `docs/adr/README.md` if missing.
3. **Scaffold** using the default stack for that type from Section 2 of AGENTS.md. Do not substitute libraries without asking.
4. **Install skills/plugins** from Section 3 that match the project type. Always: grill-me, frontend-design (if any UI), Playwright MCP (if any UI). Add Remotion or HyperFrames skills only if launch assets are in scope. Add AWS only if deploying to AWS.
5. **Set up design tokens** (Tailwind theme / CSS variables) from the brand answers, and create one sample page or screen using them.
6. **Verify.** Run the app, take screenshots at 390px and 1440px, and show the user.
7. **Report** a short checklist of what was done and anything skipped.
