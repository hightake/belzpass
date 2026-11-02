# BelzPass — Project Rules for Claude

BelzPass (belzpass.com) is a Hebrew, RTL website for publishing and searching apartments in the Kiryat Belz area — especially for holidays, but year-round too.
We are rebuilding it from WordPress + Elementor + custom plugins into a modern, code-first stack.
The new site must look identical to the current site and match the Figma design even more precisely, keep full control over data and admin, and stay easy to maintain for years.

## Stack (do not change without explicit approval)

- **Next.js** (App Router) + **TypeScript** (strict mode)
- **Payload CMS 3** for the admin panel, collections, access control and hooks
- **PostgreSQL**, hosted on Supabase, used as a plain Postgres database only. Do not use Supabase Auth or Supabase Realtime; auth and permissions live in Payload. Supabase Storage may be used for media.
- **Drizzle** via Payload's Postgres adapter
- **Tailwind CSS**, with all design values coming from tokens (see Design)
- **Motion** (motion.dev) for animations
- **Vitest** for unit tests and **Playwright** for E2E and visual comparison
- Hosting on **Vercel**

## Repository layout

```
legacy/              READ-ONLY. Old WordPress plugins, theme, DB schema. Never edit, never import from it.
design/              Extracted from Figma: tokens.json, screens/, specs/, assets/, README.md
docs/                inventory.md, data-model.md, decisions/ (one file per architectural decision)
src/
  app/(site)/        Public pages
  app/(payload)/     Payload admin (generated, minimal edits)
  collections/       Payload collection configs, one file per collection
  features/<name>/   One folder per business domain (listings, search, availability, holidays, users...)
    logic/           Pure business logic, no framework imports, fully unit-tested
    components/      UI for this feature
    server/          Server actions / queries for this feature
  components/ui/     Shared, design-system-level components only
  lib/               Small shared utilities
scripts/migration/   One-off scripts that move data from the old MySQL to Postgres
tests/
```

## Architecture principles

1. **Feature isolation.** Each business domain lives in its own `src/features/<name>/` folder. A change in one feature must not require edits in unrelated features. Features talk to each other only through explicit exported functions, never by reaching into each other's internals.
2. **Logic is separate from UI.** Business rules (pricing, availability, holiday periods, matching, validation, statuses) live in `logic/` as pure TypeScript functions with no React, Next or Payload imports.
3. **Port, don't reinvent.** Existing algorithms in `legacy/` are the source of truth for behavior. When porting a PHP algorithm, keep its behavior identical, document the source file in a comment at the top of the new file, and write parity tests that cover the same cases.
4. **Jewish calendar.** If calendar calculations are needed (holidays, Hebrew dates), use `@hebcal/core` rather than hand-written date math, unless the legacy logic does something specific that must be kept.
5. **Small, reviewable changes.** One feature or one concern per branch/PR. No drive-by refactors of unrelated code.
6. **Decisions are written down.** Any architectural choice goes into `docs/decisions/NNN-title.md` with context, decision and consequences.

## Database

- The schema is defined only through Payload collection configs. Every schema change goes through `payload migrate:create` and is committed as a migration file. Never edit the production DB by hand.
- Use real relational structure: proper tables, typed columns, relationships and indexes. Do not recreate WordPress's `postmeta` key-value pattern.
- Every collection has explicit access control. Default is deny.

## Privacy and secrets (strict)

- The site stores personal data of advertisers and users (names, phone numbers, emails).
- **Never commit real personal data.** Only the DB schema and anonymized or synthetic samples may be in the repo.
- Never commit secrets, API keys or connection strings. Use environment variables and keep `.env*` in `.gitignore`.
- Collect and expose only the personal fields a feature actually needs. Phone numbers and emails are never rendered into public HTML in a scrapeable way unless the legacy site intentionally does so — flag it if it does.
- Migration scripts read connection details from environment variables only.

## Design fidelity

- Figma is the source of truth: `design/` contains the extracted tokens, screenshots and specs.
- **No hard-coded colors, font sizes, spacing or radii in components.** Everything comes from the Tailwind theme generated from `design/tokens.json`.
- RTL first: `dir="rtl"`, `lang="he"`. Use logical properties (`ms-`, `me-`, `ps-`, `pe-`, `start`, `end`), never `left`/`right` for layout.
- Every public page must be checked against its Figma screenshot (Playwright visual comparison) at desktop and mobile widths before it is considered done.
- Respect `prefers-reduced-motion` in all animations.

## Figma usage

- Figma MCP calls are rate-limited. Be economical: fetch each node once, save the result to `design/`, and work from the saved files afterwards.
- Report how many Figma calls were used at the end of every task that used Figma.

## SEO and URLs

- Existing public URLs must keep working. Maintain `docs/url-map.md` (old URL → new URL) and implement 301 redirects for anything that changes.
- Every page has proper metadata, Open Graph and structured data where relevant.

## Code quality

- TypeScript strict, no `any` without a comment explaining why.
- ESLint + Prettier must pass. Tests must pass before a task is considered complete.
- Hebrew UI text lives in one place per feature (no scattered string literals) so wording can be changed safely.
- Prefer clear, boring code over clever code. Comments explain *why*, not *what*.

## How we work

- The project runs in phases. **Do not start a new phase without explicit approval.**
  1. Inventory (read legacy + Figma, write docs, no app code)
  2. Data model design (docs/data-model.md, reviewed before any collection is written)
  3. Project scaffold, tokens, base layout
  4. Public pages, one at a time
  5. Admin + custom business procedures
  6. Data migration script (tested repeatedly on anonymized data)
  7. SEO, redirects, performance, accessibility
  8. Parallel run and cutover
- When something in the legacy code is unclear, contradictory, or looks like a bug, **ask** — do not guess silently. Collect open questions in `docs/open-questions.md`.
- At the end of each task, summarize: what changed, what was tested, what is still open.

## Commands

(To be filled in once the project is scaffolded: dev, build, test, migrate, lint.)
