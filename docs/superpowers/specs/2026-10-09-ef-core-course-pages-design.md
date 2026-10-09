# EF Core and Advanced ASP.NET Core Course Pages Design

## Goal

Create one beginner-friendly MDX guide for each of the 13 delimiter-separated
sections in `next_pages.txt`, including the short review/transition section.
Keep all current routes stable and group the new pages consistently in the
Fumadocs sidebar and `/docs` landing page.

## Audience and editorial approach

Write for readers who may be new to programming and web development. Define
unfamiliar terms before using them, introduce code in small steps, explain
commands and framework behavior, and distinguish teaching examples from
production recommendations.

Use `next_pages.txt` as a topic outline rather than prose to reproduce. Write
original explanations and examples; omit instructor-specific language,
personal anecdotes, and attributed opinions. Correct outdated, incomplete, or
overgeneralized guidance. Use fictional, non-sensitive example data; never
include credentials, tokens, or personal identifiers.

## Page boundaries and navigation

Each delimiter-separated section becomes one page, preserving the source's
13-page structure. The brief “Reviewing everything we've done” section is a
standalone review and transition page, not merged into a neighboring lesson.

Keep routes flat in `content/docs/`. Use explicit `meta.json` ordering and
Fumadocs section separators for the sidebar. Mirror the section headings,
titles, URLs, and order on the `/docs` landing page. Preserve existing routes
and page content.

| Navigation group | Page title | Slug |
| --- | --- | --- |
| Testing and API Design | Designing API Sub-Resources | `designing-api-subresources` |
| Controllers and the Request Pipeline | Documenting Controllers with OpenAPI | `documenting-controllers-with-openapi` |
| EF Core and Data Persistence | Introduction to Entity Framework Core | `introduction-to-entity-framework-core` |
| EF Core and Data Persistence | IEnumerable and IQueryable | `ienumerable-and-iqueryable` |
| EF Core and Data Persistence | Configuring a DbContext and Migrations | `configuring-dbcontext-and-migrations` |
| EF Core and Data Persistence | Seeding Data with EF Core | `seeding-data-with-ef-core` |
| EF Core and Data Persistence | Querying Data with EF Core | `querying-data-with-ef-core` |
| EF Core and Data Persistence | Adding, Updating, and Deleting Data | `adding-updating-and-deleting-data` |
| EF Core and Data Persistence | Modeling Data with EF Core | `modeling-data-with-ef-core` |
| EF Core and Data Persistence | Reviewing the EF Core Application | `reviewing-ef-core-application` |
| Advanced ASP.NET Core Topics | Auditing Changes with EF Core | `auditing-changes-with-ef-core` |
| Advanced ASP.NET Core Topics | Integration Testing with Testcontainers | `integration-testing-with-testcontainers` |
| Advanced ASP.NET Core Topics | Authentication and Authorization in ASP.NET Core | `authentication-authorization-aspnet-core` |

The existing **Start Here** and **Minimal APIs** groups remain unchanged.
**Testing and API Design** gains the sub-resources page. **Controllers and the
Request Pipeline** gains the OpenAPI page after the controller-conversion
guide. The EF Core pages appear in source order in their own group. Auditing,
Testcontainers, and security appear in source order in **Advanced ASP.NET Core
Topics**.

## Content requirements

- **Controller OpenAPI documentation:** Explain the OpenAPI document and
  rendered UI as distinct things. Describe response metadata and XML comments,
  and identify package- or version-specific setup such as Swashbuckle rather
  than presenting it as universal ASP.NET Core behavior.
- **API sub-resources:** Compare nested routes and separately queried
  resources, including their trade-offs, response shape, route design, and
  tests. Avoid exposing sensitive employee data.
- **EF Core foundations:** Explain ORM, provider, entity, `DbContext`,
  `DbSet`, and the roles of LINQ. Clarify that an `IQueryable<T>` provider may
  translate an expression into a database query, whereas `IEnumerable<T>`
  represents in-process enumeration; explain deferred execution and when
  materialization or client-side evaluation occurs.
- **Database setup and seeding:** Show provider and connection configuration,
  dependency injection, migrations, and schema review at a beginner level.
  Distinguish model-managed seed data from environment-specific or runtime
  initialization. Do not recommend blindly applying migrations at production
  startup.
- **Queries and changes:** Explain filtering, ordering, projection,
  pagination, related data, async execution, tracking, and the change tracker.
  Show how to create, update, and delete entities without treating an
  untracked request object as a trusted database entity.
- **Modeling and review:** Explain relationships, navigation properties,
  constraints, indexes, and configuration. Use the review page to summarize
  how the sample progresses from in-memory data to persistence and to bridge
  into auditing and the final topics.
- **Auditing:** Explain when audit fields are useful and how save operations
  can set them. Derive the current actor from trusted server-side identity,
  use a testable time source, and do not trust client-supplied audit values.
- **Testcontainers:** Explain why a real database can catch provider-specific
  behavior that in-memory substitutes miss. Describe Docker prerequisites,
  container lifecycle, test-data isolation, and cleanup; do not claim that
  switching providers automatically requires a separate migration set in
  every case.
- **Authentication and authorization:** Distinguish identity from permission;
  explain claims, roles, and policies; clarify that a JWT is signed but not
  encrypted by default; and cover validation and safe handling at a high
  level. Recommend established identity protocols/providers where
  appropriate. Do not include an insecure token-issuing endpoint, token
  secrets, or a universal claim that one browser authentication pattern fits
  every application.

## Scope

- Add 13 MDX pages under `content/docs/` with meaningful `title` and
  `description` frontmatter.
- Update `content/docs/meta.json` and `content/docs/index.mdx` to include all
  13 pages once, in the approved groups and order.
- Preserve existing page slugs, content, and the unlisted `test.mdx` scaffold.
- Do not change application code, add runtime features, or modify
  `next_pages.txt`.

## Validation and acceptance

- Every delimiter-separated section in `next_pages.txt` maps to one new MDX
  page, and each expected slug appears once in both navigation surfaces.
- Sidebar and landing-page group names, card titles, URLs, and ordering match.
- Existing route names remain unchanged, and `test` remains omitted from
  navigation.
- New MDX pages have valid frontmatter and fenced code for C#, JSON, and shell
  examples; JSX/MDX parsing does not treat code as components.
- Examples are beginner-accessible, technically accurate, and contain no
  sensitive values.
- `git diff --check` passes.
- Run `npm run build` to check MDX compilation. The repository has a known
  unrelated TypeScript error at `src/components/codeblock.tsx:137`
  (`'--padding-right'` is not accepted by the style type); report it separately
  if it remains.
