# NCM Refinement Viewer

An interactive viewer for [Next-Concept Modeling (NCM)](https://github.com/HazyResearch/ncm) samples. Step through each generation level and watch text resolve from a rough sketch into finished output.

**Live page:** https://kbroadie.github.io/ncm-viewer/

## What NCM does

Most language models write left to right, one token per forward pass. NCM, from Stanford's HazyResearch lab, works coarse to fine instead. A tokenizer compresses text into a stack of codes, coarse on top and fine at the bottom, and a transformer predicts that stack from the top down. Every position within a level is predicted at once, so the whole output takes one forward pass per level.

The viewer makes that process visible:

- **Step or play** through each level of a sample.
- **Highlights** mark the words that changed since the previous level.
- **The level strip** charts word count per level, so you can see each level cover a longer sequence. Tap a bar to jump to it.
- **All levels at once** stacks every pass in one list.

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

`source`, `sourceLabel` and `sourceLang` are optional; leave them out for unconditional samples. Use `\n` inside a level for a paragraph break. New entries show up as tabs automatically.

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
