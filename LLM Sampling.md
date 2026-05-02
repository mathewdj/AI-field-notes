# LLM Sampling

Sampling is how the LLM picks the next token from a probability distribution.

After the model scores every token in its vocabulary, you get a distribution like:

```
"cat"  → 40%
"dog"  → 30%
"bird" → 20%
"fish" → 10%
```

## Sampling strategies

| Strategy | What it does |
|---|---|
| **Greedy** | Always picks the highest-probability token. Deterministic, but repetitive/boring. |
| **Temperature** | Scales the distribution. High temp (>1) flattens it (more random), low temp (<1) sharpens it (more confident). Temp=0 ≈ greedy. |
| **Top-k** | Only sample from the top k tokens, ignore the rest. Prevents picking very unlikely tokens. |
| **Top-p (nucleus)** | Only sample from the smallest set of tokens whose cumulative probability ≥ p. More adaptive than top-k. |

These are usually combined — e.g. apply temperature first, then top-p, then sample from what's left.

## Practical implications

- `temperature=0` → deterministic, good for code/structured output
- `temperature=0.7-1.0` → creative, good for writing/brainstorming
- High temp + no top-p → incoherent garbage
- The same prompt can produce very different outputs across samples — this is the non-determinism you have to design around
