# Capstone Page Design

**Goal:** Add a capstone-only portfolio entry point at `/capstone` that duplicates the main page structure while preserving the current homepage and project experience.

## Context

The existing homepage uses a three-column layout:

- left sidebar with profile content
- center feed with projects and experiences
- right column with writings

For the capstone assignment, the user wants a separate route that:

- does not affect `/`
- keeps the existing site style
- reorders sections so experience appears above writings
- presents the top five projects in a more detailed format
- adds a temporary capstone project at the top of the project list

The new capstone route should reuse the existing `/projects/[slug]` pages for real portfolio projects.

## Scope

### In Scope

- Create a new `/capstone` route
- Duplicate the homepage layout for that route only
- Build a capstone-specific feed component
- Move experience above writings on the capstone page only
- Show five detailed real projects on the capstone page
- Add a temporary capstone project card at the top of the capstone projects list

### Out of Scope

- Changing the existing homepage at `/`
- Changing existing `/projects/[slug]` detail pages
- Adding a new content collection entry for the temporary capstone project
- Reworking sitewide navigation

## Architecture

### Route

Create `src/pages/capstone.astro` as a standalone page that mirrors the current homepage composition:

- `ProfileSection` in the left column
- a capstone-specific center content area
- a right column containing writings

### New Capstone Feed

Create a dedicated component for the capstone feed rather than parameterizing the existing `MainFeed`. This keeps the current homepage completely insulated from capstone-only requirements.

Responsibilities:

- fetch project and experience collections
- sort them by date using the same conventions as the main site
- build a manual list of top five projects for the capstone page
- prepend a temporary capstone project object rendered inline

### Detailed Projects Presentation

The capstone project section should differ from the homepage by:

- rendering one temporary capstone project first
- rendering five selected portfolio projects instead of three recent ones
- using a more detailed card format with title, technologies, year, and fuller copy

The temporary capstone item should not be persisted in `src/content/projects`. It will be represented as inline data inside the capstone feed component.

## Content Decisions

The selected five real projects are:

1. `glossplusone`
2. `visionr`
3. `pointr-graph-editor`
4. `nodeflow`
5. `non-subkernel-convolution`

These provide a balanced academic portfolio across product engineering, accessibility, graph tooling, systems/ML infrastructure, and research.

The temporary capstone item should summarize current course deliverables and make clear it is an active academic project.

## Error Handling

- If any of the selected project slugs are unavailable, filter them out gracefully rather than failing the page build.
- If experience or writing entries are empty, existing collection-driven rendering behavior should still produce a stable layout.

## Verification

- Build the Astro site successfully
- Confirm `/` remains visually unchanged in code
- Confirm `/capstone` renders:
  - profile column
  - capstone projects with temporary item first
  - experience before writings
  - five real project entries
