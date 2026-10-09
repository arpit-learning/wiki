# Course Documentation Expansion and Navigation Design

## Goal

Organize the course documentation into useful sections on both the Fumadocs
sidebar and `/docs` landing page, and turn the topics in `next_pages.txt` into
separate, beginner-friendly guides. Existing routes must remain unchanged.

## Audience and editorial approach

The intended reader may be new to programming. Explain unfamiliar terms before
relying on them, introduce examples in small steps, and describe what commands
and code do. Provide practical recommendations while distinguishing simplified
teaching examples from production guidance.

Use the source file as a topic outline. Write original explanations and
examples; do not reproduce instructor-specific wording, personal anecdotes, or
attributed quotations. Review dated or inaccurate technical claims and correct
them. Do not use real sensitive personal data in examples.

## Navigation

Use Fumadocs `meta.json` page ordering with separator entries to group the
sidebar without adding folders or changing URL slugs. Mirror the group headings
and page order with section headings and cards on `/docs`.

Groups and contents:

1. **Start Here** — existing Introduction, Tooling Overview, and HTTP Overview
   pages.
2. **Minimal APIs** — What We'll Build; Minimal APIs in ASP.NET Core.
3. **Testing and API Design** — Writing Your First API Tests; Request Models
   and PUT; The Repository Pattern; Validating API Requests.
4. **Controllers and the Request Pipeline** — What Is a Controller?; Moving
   from Minimal APIs to Controllers; Logging in ASP.NET Core; Middleware and
   Filters.

Create one MDX page for each of the ten substantive topics in
`next_pages.txt`. The short “In this section, we” recap is not a standalone
lesson; incorporate its learning outcomes into the validation guide. Keep the
existing `test.mdx` scaffold file, but do not list it in the course navigation.

Suggested slugs:

| Group | Page title | Slug |
| --- | --- | --- |
| Minimal APIs | What We'll Build | `what-well-build` |
| Minimal APIs | Minimal APIs in ASP.NET Core | `minimal-apis` |
| Testing and API Design | Writing Your First API Tests | `writing-api-tests` |
| Testing and API Design | Request Models and PUT | `request-models-and-put` |
| Testing and API Design | The Repository Pattern | `repository-pattern` |
| Testing and API Design | Validating API Requests | `api-validation` |
| Controllers and the Request Pipeline | What Is a Controller? | `controllers` |
| Controllers and the Request Pipeline | Moving from Minimal APIs to Controllers | `converting-to-controllers` |
| Controllers and the Request Pipeline | Logging in ASP.NET Core | `logging` |
| Controllers and the Request Pipeline | Middleware and Filters | `middleware-and-filters` |

## Scope

- Add the ten MDX pages under `content/docs/`.
- Update `content/docs/meta.json` with the approved groups and explicit order.
- Update `content/docs/index.mdx` to show the same groups and page order.
- Do not change the route structure, application code, or existing guide content.

## Validation and acceptance

- All ten new routes appear exactly once in the sidebar and landing-page cards,
  under the approved group.
- Existing guide routes remain unchanged; the sample `test` page is not in the
  course navigation.
- New pages have meaningful frontmatter, readable MDX, and beginner-oriented
  explanations with technically accurate examples.
- `git diff --check` passes.
- Run the existing production build to verify MDX compilation. The repository
  currently has a known unrelated TypeScript error in
  `src/components/codeblock.tsx:137` (`--padding-right` is not accepted by its
  style type); report that separately if it remains.
