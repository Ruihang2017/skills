# CLAUDE.md

Guidelines for MVP work. The job is shipping the smallest thing real users can actually rely on — not a demo, not a draft, a product.

**The bias:** correctness and scope discipline over polish and breadth. If a user hits it, it has to work. Everything else can wait.

## 1. Real Users Means Real Code

A prototype can fake the backend. An MVP can't. The data is real, the state persists, the bugs are felt by humans.

- No `// FAKE:` shortcuts on anything in the user path. If a button claims to save, it saves to a real store. If a form claims to email, it emails.
- Persistence is real: a database, a real auth provider, real file storage. Pick boring, managed options (Postgres, Supabase/Clerk/Auth0, S3-compatible) unless there's a reason not to.
- Handle the errors users will actually hit: network failure on submit, duplicate signup, expired session, validation failures. Not every theoretical error — the ones in the demo path and the obvious-adjacent-paths.
- No console errors in the happy path. No silently swallowed exceptions. If something fails, the user sees a message that tells them what to do.

## 2. Cut Scope, Not Quality

One feature done well beats five features half-done. The MVP is defined by what you leave out.

- Before building, list every feature on the table. Then halve it. Then halve it again. What remains is the MVP.
- If a feature isn't core to the value proposition, it's V2. Settings pages, profile editing, notifications, exports, integrations — almost all V2.
- One auth method, not three. One payment provider, not "pluggable." One way to do the core action, not power-user shortcuts.
- Push back when scope creeps mid-build. "This adds a week and isn't in the core loop — defer?" is a sentence to say out loud.

## 3. Boring Tech, Boring Choices

MVPs die from novel-stack debugging more than from feature gaps.

- Pick the framework you'd pick if you had to ship in two weeks: Next.js or Remix on the frontend, Postgres in the back, a managed host (Vercel/Fly/Railway). No bespoke infra.
- One database. One ORM. One UI library. Don't mix `shadcn` with `MUI` because one had a nicer date picker.
- No microservices. No event buses. No queues unless there's a job that genuinely can't run inline.
- No custom auth. No custom payments. No custom anything that has a $20/month vendor.

## 4. Happy Path Solid, Edges Pragmatic

You can't cover every edge case at MVP scale. Cover the ones users will hit; degrade gracefully on the rest.

- The core loop (signup → first value → repeat use) gets the most attention. It works on every browser you care about, every input you reasonably expect.
- Edge cases get triaged: "user hits this once a week" → handle it. "User hits this once a year" → log it and move on. "Adversarial user crafts weird input" → validate at the boundary, don't sweat the rest.
- Empty states, loading states, and error states exist on every screen in the core loop. Not necessarily on admin views, not necessarily on rare flows.
- Mobile works on the core loop. It doesn't have to be beautiful on every secondary screen.

## 5. Tests Where They Earn Their Keep

MVPs don't get full test pyramids. They get tests where regressions would hurt.

- Test the core business logic: pricing, auth boundaries, data integrity, anything money- or trust-adjacent. These are the bugs that don't get forgiven.
- Skip UI snapshot tests, skip exhaustive unit tests on glue code, skip mocking everything for the sake of coverage.
- One integration test per critical flow beats fifty unit tests on the helpers around it.
- If a bug ships and gets reported, write the test before the fix. The MVP grows its test suite from real failures, not imagined ones.

## 6. Observability Before Polish

You can't fix what you can't see. Basic visibility ships with V1, not after.

- Error tracking from day one (Sentry, Rollbar, whatever — pick one and wire it up). Unhandled errors should reach you, not just the user.
- Basic analytics on the core loop: signup, activation, the one action that defines retention. Not a full funnel, not yet.
- Structured logs on the backend. Enough to answer "what happened in this user's session" when support asks.
- Skip dashboards, skip metrics on metrics. The goal is "I can debug a user's report in under 10 minutes," not "we have an observability stack."

## 7. Don't Decorate What You Can't Predict

The biggest MVP trap is building flexibility for a V2 you haven't sold yet.

- No plugin systems, no feature flags beyond the one or two you actually toggle, no settings for choices users haven't asked for.
- No premature abstraction. Two similar functions are fine. Three is when you consider extracting.
- Database schema reflects what's true today. Add columns when you need them; don't add JSON blobs "for flexibility."
- It's easier to add structure than to remove it. Ship rigid; soften under pressure.

## 8. State Tradeoffs, Then Ship

MVP work is dense with judgment calls. Surface them; don't bury them.

- When cutting scope, say what's being cut and why. "Deferring multi-user workspaces — adds a week and only 1 of 5 design partners asked." The user can overrule; they can't if it's invisible.
- When picking the boring option, say so. "Using Clerk for auth — saves ~3 days; we lose custom branding on login." Easy to redirect.
- When taking shortcuts that V2 will need to revisit, mark them: `// MVP: single-tenant assumption — revisit when we add team accounts`.
- Don't ask permission for small calls. Move. But make the medium-sized ones visible.

---

**Working signal:** real users are using it, the core loop is solid, the codebase is small enough to hold in your head, and the "what's V2" list writes itself from what you deliberately cut.
