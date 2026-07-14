Prompt for agent ai
---

See also: [[point-ai]] · [[command prompt]] · [[Web Tools MOC]]

## 1. Refactor Code React TS

See also: [[React.js]] · [[Web Tools MOC]]

```
Act as a Senior Frontend Architect.
Analyze my React + TypeScript project and propose a structured refactor plan based on SOLID principles and clean architecture.

Focus on:

- Improving code maintainability and scalability
- Removing duplication (DRY)
- Reducing coupling and increasing cohesion
- Applying SOLID principles appropriately in a frontend context
- Improving folder structure and module boundaries
- Typing improvements (remove `any`, improve generics, safer error handling)
- Consistent data-fetching and error patterns
- Component responsibility separation
- Extracting reusable hooks, utilities, and shared components

Provide:

1. High-level architectural observations
2. Code smell detection
3. A phased refactor plan (safe incremental steps)
4. Suggested folder structure improvements
5. Examples of before/after patterns (short and conceptual)

Do not rewrite the entire project.
Focus on structural improvements and long-term maintainability.
Avoid adding unnecessary dependencies unless strongly justified.
```

---

## 2. Backend API Architecture Review (Node/Express)

See also: [[building a Backend]] · [[React-and-MongoDB]]

```
Act as a Senior Backend Architect.
Review my Node.js/Express (or NestJS) API codebase for architecture, security, and scalability issues.

Focus on:

- Layering (controller → service → repository) and separation of concerns
- Input validation and sanitization at the boundary
- Consistent error handling and HTTP status codes
- Authentication/authorization patterns (JWT, session, refresh token rotation)
- N+1 queries, missing indexes, and inefficient DB access patterns
- Secrets management and environment variable hygiene
- Rate limiting, CORS, and other API hardening basics
- Logging and observability (structured logs, correlation IDs)

Provide:

1. High-level architectural observations
2. Security risk findings, ranked by severity
3. A phased improvement plan (non-breaking, incremental)
4. Suggested folder/module structure
5. Before/after examples for the most important fix

Do not propose a rewrite. Prioritize the highest-impact, lowest-risk changes first.
```

---

## 3. Database Schema & Query Review

```
Act as a Senior Database Architect.
Review my schema (SQL or MongoDB) and the queries/ORM code that access it.

Focus on:

- Normalization vs. denormalization trade-offs for the actual access patterns
- Missing or redundant indexes
- N+1 query patterns and unnecessary round-trips
- Transaction boundaries and consistency guarantees
- Migration safety (backwards-compatible, zero-downtime)
- Naming conventions and constraint usage (foreign keys, unique, not null)

Provide:

1. Schema-level observations
2. Query performance risks with concrete fixes (index or query rewrite)
3. A migration plan that can ship incrementally
4. Any concerns about data integrity or race conditions
```

---

## 4. Performance Audit (Web Frontend)

```
Act as a Senior Performance Engineer.
Audit my web app (React/Next.js) for performance issues affecting Core Web Vitals (LCP, CLS, INP).

Focus on:

- Bundle size (unused deps, missing code-splitting, barrel file over-imports)
- Render performance (unnecessary re-renders, missing memoization, expensive computations in render)
- Image/asset optimization (formats, lazy loading, responsive sizes)
- Network waterfall issues (sequential fetches that could be parallel, missing caching)
- Server-side rendering / static generation opportunities
- Third-party script impact

Provide:

1. Ranked list of findings by expected impact vs. effort
2. Concrete before/after code examples for the top 3 issues
3. Measurement plan (what to profile, what tools to use, what "done" looks like)
```

---

## 5. Accessibility (a11y) Review

```
Act as a Senior Accessibility Engineer (WCAG 2.1 AA).
Review my UI components/pages for accessibility issues.

Focus on:

- Semantic HTML vs. div-soup, correct landmark/heading structure
- Keyboard navigation and focus management (modals, menus, forms)
- ARIA usage (only where native semantics are insufficient — flag misuse)
- Color contrast and reliance on color alone to convey meaning
- Form labeling, error messaging, and screen reader announcements

Provide:

1. Findings ranked by severity (blocker / serious / minor)
2. Concrete fixes with corrected markup
3. A checklist to prevent regressions going forward
```

---

## 6. Security Review (Web App)

```
Act as a Senior Application Security Engineer.
Review this code change / codebase for security vulnerabilities, referencing OWASP Top 10 where relevant.

Focus on:

- Injection risks (SQL, NoSQL, command, XSS)
- AuthN/AuthZ gaps (missing checks, IDOR, privilege escalation)
- Sensitive data exposure (secrets in code/logs, insecure storage)
- CSRF protection and cookie/session configuration
- Dependency risk (known-vulnerable packages)
- Input validation and output encoding boundaries

Provide:

1. Findings ranked by severity with concrete exploit scenario for each
2. Minimal, targeted fixes (no unrelated refactors)
3. Notes on anything that needs a human security sign-off vs. what's safe to auto-fix
```

---

## 7. State Management Refactor (React)

```
Act as a Senior Frontend Architect specializing in state management.
Review how state is managed across my React app (useState/useContext/Redux/Zustand/Riverpod-equivalent) and identify where the chosen approach is mismatched to the problem.

Focus on:

- Local vs. global state boundaries (is everything in global state that shouldn't be?)
- Prop drilling that indicates a missing context/store
- Derived state being stored instead of computed
- Stale closures / unnecessary re-renders caused by state shape
- Server state vs. client state separation (should this be React Query/SWR instead of manual state?)

Provide:

1. A map of current state ownership vs. recommended ownership
2. Specific refactor steps, incremental and non-breaking
3. Before/after example for the worst offender
```

---

## 8. Testing Strategy

```
Act as a Senior QA/Test Architect.
Propose a testing strategy for this feature/module, given its current (lack of) test coverage.

Focus on:

- What to unit test vs. integration test vs. e2e test (test pyramid, not ice cream cone)
- Critical paths and edge cases that are currently untested
- Mocking strategy (what's safe to mock vs. what should hit a real dependency)
- Flaky test risks in the current suite

Provide:

1. A prioritized list of tests to add first (highest risk area first)
2. Example test code for the top 2 priorities
3. Suggested tooling if current setup is insufficient
```

---

## 9. Code Review (general purpose, any diff)

```
Act as a Senior Engineer doing a pull request review.
Review this diff for correctness, security, performance, and maintainability. Do not comment on style issues a linter would already catch.

Focus on:

- Logic errors and edge cases (null/undefined, empty arrays, race conditions)
- Security issues introduced by this change
- Performance regressions (new N+1 queries, unnecessary loops/allocations)
- Whether the change matches its stated intent/description
- Missing tests for the new behavior

Output format:

1. Summary (1-2 sentences: is this safe to merge?)
2. Findings, most severe first, each with file/line, the concrete failure scenario, and a suggested fix
3. Nitpicks (optional, clearly separated from real issues)
```

---

## 10. Debugging Session

```
Act as a Senior Engineer running a structured debugging session.
I will give you an error/symptom. Help me find the root cause, not just a workaround.

Process:

1. Ask for the minimal reproduction steps if not already provided
2. Form 2-3 concrete hypotheses ranked by likelihood, based on the symptom
3. For each hypothesis, propose the fastest way to confirm/deny it (log, breakpoint, test)
4. Once root cause is confirmed, propose the fix and explain why it addresses the cause, not just the symptom
5. Suggest a regression test that would have caught this
```

---

## 11. UI/Design System Consistency Audit (Tailwind/CSS)

```
Act as a Senior Design Systems Engineer.
Audit my components for design token and styling consistency.

Focus on:

- Hardcoded colors/spacing/font-sizes that should reference design tokens
- Inconsistent spacing scale or breakpoint usage across components
- Duplicate component variants that could be unified with props
- Dark mode / theming gaps

Provide:

1. Findings with file references
2. A proposed token structure if one doesn't exist
3. Migration plan that doesn't require touching every file at once
```

---

## 12. Documentation Generation

```
Act as a Senior Technical Writer / Engineer.
Generate documentation for this module/API based on the actual code (not assumptions).

Focus on:

- Purpose and responsibility of the module (the "why", not a line-by-line narration)
- Public API surface: inputs, outputs, error cases
- Non-obvious constraints, invariants, or gotchas a new engineer would hit
- A minimal usage example

Keep it concise. Do not document self-evident code. Flag anywhere the code's actual behavior seems to contradict its name or existing comments.
```
