# Profile README Visual Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the GitHub profile README into a memorable, animated portfolio teaser that communicates Luochen's product-making identity within five seconds.

**Architecture:** Keep the profile as a dependency-free Markdown experience. Add a self-contained animated SVG hero under `assets/`, use a responsive light/dark `<picture>` wrapper, and restructure the README around a short positioning statement, visual project cards, proof of open-source contribution, and a concise tools section.

**Tech Stack:** GitHub Flavored Markdown, semantic HTML supported by GitHub README rendering, inline SVG with SMIL animation.

## Global Constraints

- No JavaScript, CSS files, build system, or external runtime dependencies.
- The README must remain readable if images fail to load.
- Use only one restrained motion language: slow flowing lines and a subtle pulsing signal.
- Avoid generic section labels, badge walls, emoji, and inflated claims.
- Keep the hero alt text meaningful and preserve direct links to the repository and merged pull requests.

---

### Task 1: Add the animated hero asset

**Files:**
- Create: `assets/hero.svg`

**Interfaces:**
- Produces: A 1200×420 SVG hero with a dark graphite background, warm orange signal line, teal secondary line, and accessible text reading `Ideas → Workflows → Products`.

- [ ] **Step 1: Create the SVG asset**

Create a standalone SVG with `viewBox="0 0 1200 420"`, a dark background, a subtle grid, three large editorial words, and two slow animated paths. Use `prefers-reduced-motion` to disable motion for users who request reduced motion.

- [ ] **Step 2: Validate the SVG structure**

Run:

```bash
rg -n '<svg|viewBox|animate|prefers-reduced-motion|Ideas|Workflows|Products' assets/hero.svg
```

Expected: the asset contains the required canvas, copy, animation primitives, and reduced-motion fallback.

### Task 2: Rewrite the profile README around visual proof

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: `assets/hero.svg`.
- Produces: A profile README with a dynamic hero, selected-work cards, open-source proof, current focus, tools, and contact links.

- [ ] **Step 1: Replace the generic opening with the visual hero**

Use a `<picture>` wrapper around `assets/hero.svg`, followed by the positioning statement: `I turn messy knowledge work into AI-native products, workflows, and tools people actually use.`

- [ ] **Step 2: Add visual selected-work cards**

Use a two-column HTML table with links to `career-ops`, Codex workflows, and product experiments. Keep each card to a title, one sentence, and a proof/detail link so the section remains scannable.

- [ ] **Step 3: Compress repeated content**

Merge the existing `What I'm Building`, `Current Focus`, and `Strengths` material into `What I Build` and `Now`. Remove redundant bullets and keep the current focus time-specific.

- [ ] **Step 4: Replace the badge wall with grouped tools**

Use three text groups—AI & Automation, Product Engineering, Backend & Data—in place of the current rows of Shields badges.

- [ ] **Step 5: Add a clear closing path**

End with links to the personal site, GitHub repositories, and email/contact route if present in the current profile metadata. Do not invent a new contact address.

### Task 3: Verify rendering and publish

**Files:**
- Modify: `README.md`
- Create: `assets/hero.svg`

- [ ] **Step 1: Run local content checks**

Run:

```bash
test -s README.md
test -s assets/hero.svg
rg -n 'hero.svg|career-ops|What I Build|Now|Tools I Use' README.md
! rg -n 'QUESTION|SECTION 0[0-9]|TODO|TBD' README.md assets/hero.svg
```

Expected: all commands succeed and no banned placeholder labels are present.

- [ ] **Step 2: Inspect the diff**

Run `git diff --check` and `git diff -- README.md assets/hero.svg`. Confirm only the profile README, hero asset, and plan are changed.

- [ ] **Step 3: Commit the profile redesign**

```bash
git add README.md assets/hero.svg docs/superpowers/plans/2026-07-10-profile-readme-visual-redesign.md
git commit -m "feat: redesign profile README with animated hero"
```

- [ ] **Step 4: Push to GitHub**

```bash
git push origin main
```

Expected: the profile repository's default branch is updated with the new README and asset.
