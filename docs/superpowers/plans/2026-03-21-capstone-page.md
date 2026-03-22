# Capstone Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a new `/capstone` page that mirrors the homepage layout while showing a capstone-specific projects section and preserving the current `/` route.

**Architecture:** Implement a standalone `src/pages/capstone.astro` page that reuses the existing layout and profile/writing sections while introducing a new capstone-only feed component. Keep all capstone-specific ordering and temporary project content isolated to the new feed so the existing homepage stays unchanged.

**Tech Stack:** Astro, Astro content collections, TypeScript, Tailwind utility classes

---

### Task 1: Create the capstone feed component

**Files:**
- Create: `src/components/sections/CapstoneFeed.astro`
- Reference: `src/components/sections/MainFeed.astro`
- Reference: `src/lib/content.ts`

- [ ] **Step 1: Create the selected project list**

Define the five project slugs inline and resolve them from the `projects` collection while preserving a fixed order:

```ts
const capstoneProjectSlugs = [
  'glossplusone',
  'visionr',
  'pointr-graph-editor',
  'nodeflow',
  'non-subkernel-convolution',
];
```

- [ ] **Step 2: Create the temporary capstone item**

Add an inline object for the academic capstone placeholder with title, summary, deliverables, status label, and no dependency on the content collection.

- [ ] **Step 3: Render the projects section**

Render the temporary capstone card first, then render the five selected real projects in a more detailed layout with:

- title
- year
- technology list
- longer descriptive copy
- link to `/projects/[slug]`

- [ ] **Step 4: Render the experiences section**

Reuse the current sorting/filtering behavior and show the top experiences under the projects section.

- [ ] **Step 5: Keep styling isolated**

Copy only the leader-link and section styles needed for the new component so changes do not affect `MainFeed.astro`.

### Task 2: Add the new `/capstone` page

**Files:**
- Create: `src/pages/capstone.astro`
- Reference: `src/pages/index.astro`

- [ ] **Step 1: Duplicate the page shell**

Reuse the same `BaseLayout` and grid structure from `src/pages/index.astro`.

- [ ] **Step 2: Replace the main feed**

Use `CapstoneFeed` in the main content column.

- [ ] **Step 3: Reorder right-column content**

Place experience above writings for the capstone route only. If needed, render a second dedicated experience section component or include experiences in the capstone feed and keep writings on the right.

- [ ] **Step 4: Preserve homepage isolation**

Do not modify the current `src/pages/index.astro` behavior or imports unless a shared extract is strictly necessary.

### Task 3: Verify build and lint state

**Files:**
- Modify if needed: `src/components/sections/CapstoneFeed.astro`
- Modify if needed: `src/pages/capstone.astro`

- [ ] **Step 1: Run diagnostics**

Check edited files for lints after implementation.

- [ ] **Step 2: Run production build**

Run:

```bash
npm run build
```

Expected: Astro build succeeds without errors.

- [ ] **Step 3: Fix issues if present**

Resolve any typing, import, or template issues surfaced by build or lints.
