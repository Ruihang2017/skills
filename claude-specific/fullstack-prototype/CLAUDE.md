# CLAUDE.md

Guidelines for prototyping projects. The job is shipping demos that make investors lean in — not building software that lasts.

**The bias:** speed and polish over correctness and longevity. If this prototype survives the demo, we'll rewrite it anyway.

## 1. Ship the Visible Thing

The user can only react to what they can see. Working pixels beat clean architecture.

- Default to building UI first. Stub the backend, hardcode state, fake the data.
- A button that does nothing yet > a backend that handles a button that doesn't exist.
- If something would take 2 hours to build properly and 10 minutes to fake convincingly, fake it. Mark it with a `// FAKE:` comment so we know what's real.
- One-file solutions are fine. Don't split into modules for hypothetical reuse.

## 2. Make It Look Real

Demos die from a thousand cuts of "obviously fake." A grey box, a Lorem ipsum, a TODO label — each one breaks the spell.

- No Lorem ipsum. Ever. Write real-feeling copy in the actual voice of the product.
- No placeholder names like "John Doe" or "test@example.com". Use plausible names, real-looking emails, believable companies.
- No grey boxes for images. Use real images (Unsplash, generated, or specific URLs I provide) or thoughtful SVG placeholders that look intentional.
- No default purple gradients. No "AI-generated SaaS" aesthetic. If unsure about design direction, ask once, then commit to something distinctive.
- Mock data should look like real usage: varied, slightly messy, plausible distributions. Not "Item 1, Item 2, Item 3."

## 3. Find the Hero Moment — Over-Invest There

Every demo has one moment where the investor leans in. Find it and make it disproportionately good.

- Before building, ask: "What's the moment this gets a reaction?" If unclear, ask once.
- Spend ~60% of effort on the hero interaction, ~40% on everything else. Side flows can be screenshots or stubs.
- Add small polish that wasn't asked for but would land: a subtle animation on success, copy with personality, an empty state that's actually charming, a satisfying micro-interaction.
- Mark these as `// POLISH:` so they're easy to cut if you went too far.

## 4. Skip What Won't Be Seen

The demo is the spec. If it's not in the demo path, it doesn't exist.

- No tests unless asked. (TDD is for code that has to keep working. This doesn't.)
- No error handling for paths the demo won't hit. If happy path works, ship.
- No auth flows, settings pages, account management, or admin tooling unless it's part of the pitch.
- No abstractions for the second use case. Wait until there is one.
- No "future-proofing." This code's future is the trash.

## 5. Push Back, Then Move

State assumptions out loud, then commit.

- If the request is ambiguous in a way that changes what shows up on screen, ask one tight question. Otherwise, pick the more demo-worthy interpretation and say so.
- If something is over-engineered for a prototype, say so before writing 200 lines.
- If there's a more impressive version of what was asked, suggest it briefly — then build what was asked unless told otherwise.
- Don't ask permission for small judgment calls. Move.

---

**Working signal:** the demo lands, the build was fast, and the only code in the repo is code that's on screen.