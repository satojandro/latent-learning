# Latent Learning: notes for Claude

## What this is
An interactive storybook that retells the Transformer Circuits papers (transformer-circuits.pub) for curious adults and ambitious teenagers with no maths background. It's colourful, animated, and told as one continuous story of discovery over time. Chapters are listed in README.md.

## Depth and tone (the owner's brief)
Don't dumb things down to the lowest common denominator. Aim to awe and impress, and draw people in deeper and deeper, slowly, so there's real learning. Readers should feel challenged and rewarded as they learn new things.
- Every scene opens accessibly, then climbs: story layer → "Go deeper" layers with the real mechanism, the paper's own terms, numbers and (once, translated into plain words) its notation.
- Stay close to the papers: their actual question, experiments, key figures (redrawn in our own style, ideally as live toys), short attributed quotes, and how strong the authors judged each piece of evidence. Point to the section of the paper so people can read alongside.
- Challenge the reader: "predict before you press" moments, puzzles, and a reveal that rewards them.

## Ground rules
- **Accuracy first.** The style is a children's book; the facts are not simplified into wrong ones. Check every claim against the paper. Label what's established ("Known") and what's open or speculative ("Unknown").
- **Clearly unofficial.** Use our own name and look. Never imitate Anthropic's branding or the site's design. Credit and link the original paper in every chapter.
- **Original words and visuals.** Don't copy figures or text from the papers.
- **Real toys where possible.** Prefer interactives that compute the real thing (e.g. the live toy model in Chapter 3) over decorative animations.

## The recurring cast (keep consistent across chapters)
- **The case file**: the residual stream, what the model is thinking about right now.
- **The clerks**: the layers. Each reads the file, adds notes, passes it on.
  - **Messengers** = attention heads: look at *earlier* files and copy notes across. Two jobs: where to look (QK) and what to copy (OV).
  - **Thinkers** = MLP layers: work on one file alone.
- **One file per word**: each token has its own case file; the last file is read for the next-word guess.
- Chapter 1's running example: "Ms Okafor … thanked Ms" and a 25-sentence courtroom story (Ms Reyes, Mr Chen, Dr Patel). Reuse it in Chapter 2 for induction heads.
- **The concepts**: features, stored as arrows (directions).
- **The desks**: the available dimensions/directions.
- Analogies already used: hot-desking (superposition), see-saw (antipodal pairs), "ignoring the whispers" (ReLU filtering out interference), the detective/judge preferring the account with the fewest moving parts (sparsity in dictionary learning), the roster of who sits at each desk (the feature dictionary), legal taxonomy (feature splitting), a dial / clamping (feature steering), "a lawyer understands fraud without committing it" (representing a concept is not acting on it), the but-for test (interventions), a careful witness who says "I don't recall" (the can't-answer default), an advocate arguing backwards from a chosen conclusion (unfaithful reasoning).

## Structure of a chapter
Story hook (the puzzle researchers faced), scenes with interactive toys, "Known / Unknown" cards, a teaser for the next chapter, credits.

## Tech
- `index.html` is a single self-contained page: inline CSS/JS, Google Fonts only, no build step. It has no `<!doctype>`/`<html>`/`<head>` tags because it's also published as a claude.ai Artifact, which adds that skeleton.
- Colours are theme tokens with light and dark variants. Respect `prefers-reduced-motion`. Must work at phone width.

## About the author
The project owner is a lawyer with a crypto background who now works with AI agents, and is learning mechanistic interpretability from scratch. Analogies from law and crypto land well.

## Editing chapters in parallel
Several chapters may be edited at once on separate branches, all in `index.html`. To keep merges clean:
- Edit only inside your chapter's `<article id="…">…</article>` and your chapter's existing JS blocks in the shared script. Leave every `/* ---------- … ---------- */` marker line where it is.
- Put new CSS in a `<style>` at the top of your article, with selectors scoped to `#your-article-id`.
- Put new JS in a `<script>` at the bottom of your article, inside `document.addEventListener('DOMContentLoaded', () => { … })`, using `window.LL` (`LL.C` colours, `LL.css`, `LL.arrow`, `LL.redrawers`, `LL.shared`, `LL.reduce`).
- Don't edit the timeline strip, the hero, the footer, README.md or CLAUDE.md; suggest changes in the PR description instead. Keep `LL.shared.court` (Chapter 1) working: Chapters 2, 5 and 6 use it.

## Workflow
- **One commit per chapter.** When a chapter is finished and checked, commit it on its own (index.html plus any README/CLAUDE.md updates for it) and push to `main`. Don't bundle two chapters in one commit. Small fixes to an existing chapter get their own commit too.
- After pushing, republish the claude.ai Artifact so the live page matches the repo.
