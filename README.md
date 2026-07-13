# starseed-carousel

Private assets + instructions for the StarSeedSoul Instagram carousel generator (Cloud
Routine reads from this repo). Not public.

## Structure

- `BRAND.md` — single source of truth for positioning, voice, audience, hard bans.
- `starseed_carousel_generator.md` — the design-system instructions (style, copy
  rules, layout variety, export).
- `carousel-assets/profile.jpg` — avatar for callout headers.
- `carousel-assets/photos/` — cosmic visuals for slides. **Olesya refills this in
  batches.** Drop images here; the generator picks from whatever is available and
  fresh. Fewer photos than slides is fine — the rest become clean text-only slides.
- `references/` — copywriting reference files the generator consults.

## How the automated flow uses it

1. Telegram message with a topic to **@starseedsoultype_bot** → Supabase forwarder
   (`starseed-carousel-forward` on the twin-frequency project) → Cloud Routine API
   trigger.
2. The Cloud Routine reads `BRAND.md`, `starseed_carousel_generator.md`, and the
   photos in `carousel-assets/photos/`, writes the copy, builds the HTML, exports
   1080×1350 PNGs, and sends them back to Telegram together with an English caption.
3. Used photos are tracked via the `starseed-used-photos` edge function so they are
   never repeated.

## Adding photos

- Web: **Add file → Upload files**, drag images into `carousel-assets/photos/`, commit.
- Local: drop files into `carousel-assets/photos/`, then `git add`, `git commit`, `git push`.
