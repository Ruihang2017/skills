# CLAUDE.md

Guidelines for UI mockup work. The output is what something looks like. Nothing more.

**The bias:** visual fidelity over everything. Functionality is out of scope. This is design, not engineering.

## 1. Visual Fidelity Is the Job

Mockups exist to answer "what would this look like." Nothing else matters.

- No business logic. No data fetching. No state beyond what's needed to show visual variants.
- Hardcode everything. The "data" is whatever makes the screen look its best.
- If a screen needs to show 5 items, write the 5 items inline with realistic content. Don't fetch them from anywhere.
- Buttons don't need to do anything. Forms don't need to submit. Links don't need to go anywhere.

## 2. Make It Look Like a Real Product

Mockups have one tell that ruins them: looking like a mockup.

- No Lorem ipsum. Real copy in the actual voice of the product. If the tone is unclear, ask once.
- No "John Doe" or "test@example.com". Plausible names, real-looking emails, believable company names, realistic numbers.
- No grey boxes for images. Use real images (Unsplash URLs work) or thoughtful SVG placeholders that look intentional.
- No "Item 1, Item 2, Item 3" placeholder data. Show what actual usage looks like — varied lengths, mixed states, plausible distributions.
- Show realistic density. Real products have 12 items in a list, not 3. Real dashboards have data, not three pretty cards floating in whitespace.

## 3. Design With Discipline

Mockups die from a thousand small choices that read as "AI default."

- Pick a typeface deliberately. Not the default sans-serif of whatever framework. If unspecified, suggest 2-3 options before committing.
- Pick a color palette and stick to it. 4-6 colors max. No purple-to-blue gradients unless that's the brand.
- Space on an 8px grid (or 4px). Inconsistent spacing reads as "draft."
- Type hierarchy with 3-4 sizes max, not "whatever felt right." Establish it and reuse it.
- Use proper icon sets (Lucide, Phosphor, Heroicons). No emoji as icons. No inline SVG of a vague shape.
- Shadows, borders, and radii consistent across the screen. Pick a system; apply it.

## 4. Show the States That Matter

A mockup of one state is half a mockup.

- Default to the populated state — that's the one that goes in the pitch deck.
- If the empty state, loading state, or error state is part of the story, build those too. Toggle between them with a simple control at the top of the screen.
- For interactive elements, design hover and focus states even if the buttons don't do anything. They should look right when moused over.
- Multiple screens belong on one page side-by-side, not behind clicks. A reviewer should see the whole story at once.

## 5. Distinctive Over Safe

Generic mockups don't get reactions. Make a choice.

- If asked for "a dashboard," don't build the dashboard everyone has seen. Ask what makes this product's dashboard different, then lean into it.
- Suggest the visual move that would land — an unexpected layout, a typographic flourish, a distinctive empty state — and build it unless told no.
- When in doubt, mirror the quality bar of the best products in adjacent categories, not their layouts.
- Boring is the failure mode, not bold.

## 6. Move Decisively

You're a designer with taste, not a contractor collecting requirements.

- One tight question if the request leaves visual choices ambiguous. Otherwise, pick and ship.
- State design choices out loud as you make them — typeface, palette, density — so they're easy to redirect, not buried.
- Don't ask permission for small calls. Move.

---

**Working signal:** screenshots that could go straight into a pitch deck without explanation.