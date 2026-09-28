# AI-Powered Code Suggester

Fine-tuned DistilGPT2 for Python code completion — give it the start of a function, it predicts what comes next.

## Problem Statement

GitHub Copilot showed that a model trained on real code can genuinely speed up development by suggesting completions as you type. Full CodeLlama-7B fine-tuning needs a paid GPU, so this project uses DistilGPT2 instead — much smaller, still learns the same code-completion skill, and trains fine on a free Colab GPU.

## Dataset

Built directly from the **Python standard library source code** installed on the training machine (via `inspect.getsource`) — zero external dataset dependency, so this step can never fail due to a broken download. ~1,000 real Python functions collected this way. (Code optionally tops itself up with a larger dataset from HuggingFace if one is reachable.)

## What It Builds

- A DistilGPT2 model fine-tuned to complete Python code given the code written so far
- A tokenizer-length optimization step (95th-percentile sizing) to reduce padding waste
- A latency benchmark for real-time autocomplete feasibility
- A saved, reloadable model artifact

## Results (from an actual training run)

| Metric | Value |
|---|---|
| Training examples | 998 real Python functions |
| Training epochs | 3 |
| Final training loss | 1.95 |
| Average suggestion latency | **584 ms** |
| Training time | ~1.7 min on a free Colab T4 |

## Tech Stack

Python · HuggingFace Transformers · Google Colab (free T4 GPU)

## How to Run

1. Open the notebook in Google Colab
2. Runtime → Change runtime type → T4 GPU
3. Run all cells top to bottom
4. Enter a free [Groq API key](https://console.groq.com/keys) when prompted (used for an optional AI helper, not required for the core training pipeline)

## Repo Structure

```
ai-code-suggester/
├── AI_Powered_Code_Suggester.ipynb
└── README.md
```

## Disclaimer

Built as a learning/portfolio project on a small dataset. Not a drop-in Copilot replacement — a much larger dataset and longer training run would be needed for production-grade suggestions.

---
By Akshat Kesharwani
