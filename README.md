# Alpha Creative Guardrails

A polished, single-page MVP for Alpha's Assets workflow: turn a grounded Morrow marketing brief into a publishable Instagram asset while keeping facts, logo, product image, and exact offer copy correct.

## Product thesis

> Spend model budget where creativity is valuable; use deterministic systems where correctness is valuable.

## Architecture

`Brief → structured Creative Contract → reference layout interpretation → demo visual layer → deterministic SVG composition → QA → publishable asset`

The background and visual atmosphere are intentionally implemented as a **local demo-generation fallback**. The approved product illustration, Morrow logo, price, headline, CTA, and composition-critical positioning are deterministic SVG layers. No external model or API is called.

## Key decisions

- **Creative Contract:** visible grounding separates protected assets/facts from editable variables and creative direction.
- **Reference guardrail:** the prototype applies only layout, hierarchy, whitespace, and composition signals, not reference brand identity.
- **QA:** checks the exact required copy, approved assets, 1:1 format, safe margins, and brand compliance.
- **Targeted repair:** the test controls demonstrate reference contamination protection, an unsupported-claim block, and a surgical price edit.
- **Surgical edit:** the price change updates the `price-layer` only. It does not regenerate the background, logo, bottle, layout, headline, or CTA.

## Run locally

```bash
npm install
npm run dev
```

Create a production build with `npm run build`, then optionally inspect it using `npm run preview`.

## Environment variables

Copy `.env.example` to `.env.local` only if an optional generation provider is added later. `IMAGE_GENERATION_API_KEY` is a placeholder; this prototype requires no credentials and keeps working without it. Any future provider must be invoked by a server-side route, never browser code.

## Deploy to Vercel

1. Push only the source repository to GitHub.
2. Import it into Vercel; Vercel detects Vite automatically.
3. Use build command `npm run build` and output directory `dist`.
4. Add optional provider secrets in Vercel Environment Variables, never in source or GitHub.

## Security and limitations

The UI bounds the editable brief to 600 characters and uses React text rendering—no unsafe HTML injection or uploads are accepted. `.env` files, build output, logs, and dependencies are ignored. This is a product prototype: QA is deterministic against the structured composition rather than computer-vision validation, the bottle is an embedded approved vector illustration, and the visual-generation stage is explicitly simulated rather than an image-model integration.
