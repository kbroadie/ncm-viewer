# NCM Refinement Viewer

An illustrated, interactive, plain-language story about [Next-Concept Modeling (NCM)](https://arxiv.org/abs/2610.14162), a way of generating text developed by researchers at Stanford. Instead of writing one word at a time, NCM sketches a whole passage and sharpens it in about a dozen passes.

**Read it:** https://kbroadie.github.io/ncm-viewer/

## Credit

Next-Concept Modeling is the work of Hermann Kumbong, Ishan S. Khare, Iddah Mlauzi, Andrew Woen, Charles Ding, E. Kelly Buchanan, Simran Arora, Azalia Mirhoseini and Christopher Ré. The research, models and examples are theirs, published in [HazyResearch/ncm](https://github.com/HazyResearch/ncm) under the MIT license.

The story, illustrations and interactive graphics are an independent project by Kevin Broadie and are not affiliated with the authors.

## What's in the story

The page is a single long scroll. In each major section a graphic sticks in place while short notes scroll past and change it.

- **A story that writes itself as you scroll.** One of the researchers' models writes a children's story, pass by pass.
- **A typewriter, a scratch-off card and a sketch artist.** Word-by-word, diffusion and NCM generation translate the same German sentence, one at a time and then as a race. Only the NCM lane uses real model output.
- **How do you sketch with words?** Map zoom levels illustrate the layers, alongside each model's real layer sizes from the researchers' configuration files.
- **Three models, three jobs.** The published story, summary and translation examples, with their inputs, stepping through the funniest mid-draft mistakes before handing the controls to the reader.
- **Every square is one step.** A unit chart of step counts reported in the paper, then measured speedups, a 16-drafts illustration, a Sudoku illustration, limits and a highway illustration of why parallel work matters.

## How the data was prepared

The NCM repository doesn't publish pass-by-pass text as data, so each pass was transcribed from the coarse-to-fine animation in that repository (`assets/coarse_to_fine.gif`). Highlights are computed in the browser by comparing each pass with the one before it, word by word. Speed, quality, Sudoku and training figures are quoted from the paper. The Sudoku and highway graphics illustrate ideas and aren't model output.

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
