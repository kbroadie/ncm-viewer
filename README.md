# Watching Text Resolve

**An Interactive Companion to Next-Concept Modeling**

A paper-format web page with interactive figures for [Next-Concept Modeling (NCM)](https://github.com/HazyResearch/ncm). It decodes the published samples level by level, charts the level schedules of six released models, and compares pass counts with autoregressive and diffusion generation.

**Read it:** https://kbroadie.github.io/ncm-viewer/

## What NCM does

Most language models write left to right, one token per forward pass. NCM, from Stanford's HazyResearch lab, works coarse to fine instead. A tokenizer compresses text into a stack of codes, coarse on top and fine at the bottom, and a transformer predicts that stack from the top down. Every position within a level is predicted at once, so the whole output takes one forward pass per level.

The page follows the structure of an ML paper (abstract, background with equations, results, limitations and references) and has three interactive figures:

1. **A sample, level by level.** Step or play through each level of a published sample. Highlights mark the words that changed since the previous level, and the level strip charts word count per level. Tap a bar to jump to it, or open "All levels at once" to see every pass stacked.
2. **The level schedule.** How many code positions each level holds, for six of the released models (TinyStories, XSum, WMT14, Sudoku, LM1B and OpenWebText), read straight from the NCM repo's `config/eval` files.
3. **Counting passes.** The WMT14 translation produced three ways: autoregressive, diffusion and NCM. The NCM lane plays the real sample; the other two are simulations of the same sentence. Below it, pass counts and wall-clock speedups reported in the paper.

## Samples

Three samples from the NCM repo are included:

| Sample | Task | Levels |
| --- | --- | --- |
| TinyStories | Unconditional story generation | 12 |
| XSum | News summarization | 9 |
| WMT14 | German to English translation | 11 |

The NCM repo doesn't publish per-level text as data, so I transcribed each level from the coarse-to-fine animation in that repo (`assets/coarse_to_fine.gif`). Highlights are computed in the browser with a word-level diff against the previous level, so they approximate the original animation's highlighting rather than reproduce it exactly.

## Adding samples

All sample data lives in [`samples.json`](samples.json). Each entry looks like this:

```json
{
  "id": "xsum",
  "name": "XSum",
  "tag": "summary",
  "task": "summarization",
  "outputLabel": "NCM output · summary",
  "sourceLabel": "Article (excerpt)",
  "sourceLang": "en",
  "source": ["First paragraph of the input.", "Second paragraph."],
  "levels": ["text at level 1", "text at level 2", "..."]
}
```

`source`, `sourceLabel` and `sourceLang` are optional; leave them out for unconditional samples. Use `\n` inside a level for a paragraph break. An optional `notes` object, keyed by level number, shows a callout under that level. New entries show up as tabs automatically.

Level schedules live in the same file under `schedules`, one entry per model with its `levels` (positions per level), `codebook` size and source `config` path.

## Running locally

The page loads `samples.json` with `fetch`, so serve the folder rather than opening the file directly:

```sh
python3 -m http.server
```

Then open http://localhost:8000.

## Credits

- NCM and the original samples: [HazyResearch/ncm](https://github.com/HazyResearch/ncm), MIT license.
- Paper: Kumbong et al., *Next-Concept Modeling: Fast, Parallel Coarse-to-Fine Text Generation*, 2026. [arXiv:2610.14162](https://arxiv.org/abs/2610.14162)

This viewer is an independent project and isn't affiliated with the NCM authors.

## License

MIT. See [LICENSE](LICENSE).
