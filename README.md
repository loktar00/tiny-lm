# SMALL LANGUAGE: watch a tiny model learn to write

**Live demo:** https://loktar00.github.io/tiny-lm/

A complete, from-scratch language model that trains **live in your browser**: no libraries, no server, no GPU. One HTML file, plain JavaScript.

It starts as random noise and, over a few thousand steps, learns to write short fables and rhymes, one character at a time. You can watch the loss fall, read its samples improve, change the settings, and type your own opening for it to continue.

## What's inside

- **Its own autograd engine:** tensors, backprop and every gradient, written by hand in JavaScript.
- **A small GPT** (decoder-only transformer), character level:
  - default size: 2 layers, 64-dim, 4 heads, 64-character context, **about 108k parameters**;
  - two larger presets: 3 layers × 96-dim, and 4 layers × 128-dim;
  - pre-norm LayerNorm, causal self-attention, 4× MLP with GELU.
- **Training recipe:**
  - AdamW (β1 0.9, β2 0.95, weight decay 0.01 on weights only);
  - learning rate 0.004 with a 30-step warmup, then cosine decay over 3,000 steps;
  - gradient clipping at norm 1;
  - batch size 8 (adjustable);
  - cross-entropy on the next character.
- **Data:** a small built-in corpus of classic public-domain fables and nursery rhymes, split by story into train and validation.
- **Sampling:** temperature sampling (default 0.7), continuing from any prompt you type.
- Training runs in a **Web Worker**, so the page stays smooth.

It is nanoGPT's idea shrunk to the size of a web page.

## Run it

Open `index.html` in any modern browser. That's it.

## How it was made

The whole page, including the autograd engine, the model, the trainer and the UI, was written by **Qwen 4 (early access)**. It worked in an agentic loop: it wrote the page, opened it in a browser, took screenshots, judged its own work and fixed it until it was satisfied.

## License

MIT
