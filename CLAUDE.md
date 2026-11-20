# Latent Learning: notes for Claude

## What this is
An interactive storybook that retells the Transformer Circuits papers (transformer-circuits.pub) for curious adults and ambitious teenagers with no maths background. It's colourful, animated, and told as one continuous story of discovery over time. Chapters are listed in README.md.

## Ground rules
- **Accuracy first.** The style is a children's book; the facts are not simplified into wrong ones. Check every claim against the paper. Label what's established ("Known") and what's open or speculative ("Unknown").
- **Clearly unofficial.** Use our own name and look. Never imitate Anthropic's branding or the site's design. Credit and link the original paper in every chapter.
- **Original words and visuals.** Don't copy figures or text from the papers.
- **Real toys where possible.** Prefer interactives that compute the real thing (e.g. the live toy model in Chapter 3) over decorative animations.

## The recurring cast (keep consistent across chapters)
- **The case file**: the residual stream, what the model is thinking about right now.
- **The clerks**: the layers. Each reads the file, adds notes, passes it on.
- **The concepts**: features, stored as arrows (directions).
- **The desks**: the available dimensions/directions.
- Analogies already used: hot-desking (superposition), see-saw (antipodal pairs), "ignoring the whispers" (ReLU filtering out interference).

## Structure of a chapter
Story hook (the puzzle researchers faced), scenes with interactive toys, "Known / Unknown" cards, a teaser for the next chapter, credits.

## Tech
- `index.html` is a single self-contained page: inline CSS/JS, Google Fonts only, no build step. It has no `<!doctype>`/`<html>`/`<head>` tags because it's also published as a claude.ai Artifact, which adds that skeleton.
- Colours are theme tokens with light and dark variants. Respect `prefers-reduced-motion`. Must work at phone width.

## About the author
The project owner is a lawyer with a crypto background who now works with AI agents, and is learning mechanistic interpretability from scratch. Analogies from law and crypto land well.
