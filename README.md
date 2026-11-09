# NCM Refinement Viewer

An illustrated, interactive, plain-language story about [Next-Concept Modeling (NCM)](https://arxiv.org/abs/2610.14162), a way of generating text developed by researchers at Stanford. Instead of writing one word at a time, NCM sketches a whole passage and sharpens it in about a dozen passes.

**Read it:** https://kbroadie.github.io/ncm-viewer/

## Credit

Next-Concept Modeling is the work of Hermann Kumbong, Ishan S. Khare, Iddah Mlauzi, Andrew Woen, Charles Ding, E. Kelly Buchanan, Simran Arora, Azalia Mirhoseini and Christopher Ré. The research, models and examples are theirs, published in [HazyResearch/ncm](https://github.com/HazyResearch/ncm) under the MIT license.

The story, illustrations and interactive graphics are an independent project by Kevin Broadie and are not affiliated with the authors.

## What's in the story

The page is a single long scroll built from pinned scenes. Each scene holds still while scrolling advances its animation, then releases when it's done. Every scene has its own color.

- **Pictures first.** A pixel picture sharpens from one block to full detail, the image-generation idea the story is built on.
- **A story that writes itself.** One of the researchers' models writes a children's story, pass by pass, centered on screen.
- **Three ways to write a sentence.** An LLM (typewriter), a diffusion model (scratch-off card) and NCM (sketch artist) translate the same German sentence. Only the NCM lane uses real model output.
- **What does a rough sentence look like?** The translation's slots fill pass by pass, with the draft each set of slots unpacks into. Slot counts come from the researchers' configuration files.
- **Try it yourself.** Scrub through the published examples and jump to the bloopers.
- **So how much faster is it?** A unit chart of step counts reported in the paper, measured speedups and a 16-drafts illustration.
- **Sudoku.** An LLM-style model writing a well-known puzzle's answer cell by cell, beside NCM's 12 passes and slot counts.
- **Why your graphics card cares.** Memory trips per short story for an LLM and for NCM, followed by the memory shortage and what it means for data centers and local AI.

## How the data was prepared

The NCM repository doesn't publish pass-by-pass text as data, so each pass was transcribed from the coarse-to-fine animation in that repository (`assets/coarse_to_fine.gif`). Highlights are computed in the browser by comparing each pass with the one before it, word by word. Speed, quality, Sudoku and training figures are quoted from the paper. The pixel picture, Sudoku scene and memory scene illustrate ideas and aren't model output; see the Notes on the page for details.

## Data file

Examples and layer schedules live in [`samples.json`](samples.json). Each example has a `task`, an `inputLabel` and `inputNote`, an optional `source` (the input text), an `outputLabel`, a `levels` array with the text after each pass, and optional `notes` keyed by pass number. Each schedule has a plain `label`, its `levels` (slots per layer), `codebook` size and source `config` path.

## Running locally

The page loads `samples.json` with `fetch`, so serve the folder rather than opening the file directly:

```sh
python3 -m http.server
```

Then open http://localhost:8000.

## License

The code in this repository is MIT licensed. See [LICENSE](LICENSE).
