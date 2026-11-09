# NCM Refinement Viewer

An interactive explainer for [Next-Concept Modeling (NCM)](https://arxiv.org/abs/2610.14162), a coarse-to-fine text generation method developed by researchers at Stanford.

**View it:** https://kbroadie.github.io/ncm-viewer/

## Credit

Next-Concept Modeling is the work of Hermann Kumbong, Ishan S. Khare, Iddah Mlauzi, Andrew Woen, Charles Ding, E. Kelly Buchanan, Simran Arora, Azalia Mirhoseini and Christopher Ré. The research, models and samples are theirs, published in [HazyResearch/ncm](https://github.com/HazyResearch/ncm) under the MIT license.

This visualizer is an independent project by Kevin Broadie and is not affiliated with the authors.

## What the page covers

The page explains NCM in four sections, each written at three depths:

- **Overview:** plain language, for any reader.
- **Technical:** how the method works, for engineers and the technically curious.
- **Expert:** equations, ablations and caveats, for machine learning researchers.

A reading-depth control opens every technical or expert layer at once, and each layer can also be expanded on its own.

Three interactive figures support the text:

1. **A sample, pass by pass.** The published TinyStories, XSum and WMT14 samples, decoded after every pass, with changed words highlighted.
2. **Level schedules.** Positions per level for six released models, read from the NCM repository's `config/eval` files.
3. **Counting passes.** The WMT14 translation produced word by word, by diffusion and by NCM. The NCM lane replays the real sample; the other two are simulations.

## How the data was prepared

The NCM repository doesn't publish per-pass text as data, so each pass was transcribed from the coarse-to-fine animation in that repository (`assets/coarse_to_fine.gif`). Highlights are computed in the browser with a word-level diff against the previous pass, so they approximate the original animation's highlighting. Speed figures are quoted from the paper.

## Adding samples

All data lives in [`samples.json`](samples.json). Each sample looks like this:

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
  "levels": ["text after pass 1", "text after pass 2", "..."]
}
```

`source`, `sourceLabel` and `sourceLang` are optional; leave them out for unconditional samples. Use `\n` inside a level for a paragraph break. An optional `notes` object, keyed by pass number, shows a callout under that pass. New samples show up as tabs automatically.

Level schedules live in the same file under `schedules`, one entry per model with its `levels` (positions per level), `codebook` size and source `config` path.

## Running locally

The page loads `samples.json` with `fetch`, so serve the folder rather than opening the file directly:

```sh
python3 -m http.server
```

Then open http://localhost:8000.

## License

The visualizer code is MIT licensed. See [LICENSE](LICENSE).
