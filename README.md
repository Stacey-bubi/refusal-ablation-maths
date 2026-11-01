# Refusal ablation and maths

Chat models refuse certain questions. Inside the model there's a direction that
carries that refusal, and subtracting it makes the model answer almost anything.
People call this abliteration. The worry is that it also wrecks the model's
maths, so I checked.

## Why

Labonne's blog post, where most people learn the method, says performance drops
after the edit and points at GSM8K (grade-school maths problems). No numbers in
the text, one model.

A paper comparing four tools (arXiv:2512.13655) leads with maths being the most
fragile skill, quoting a GSM8K swing of +1.5 to -18.8 points. But only three of
its models have before-and-after rows, and its own margin of error is about 1.3
points. Nine of its ten results fall inside that. The alarming number is one
tool on one model.

GSM8K also takes a long chain of steps, and one bad step ruins the answer. A
model slightly worse at everything would fail it first. So a GSM8K drop alone
tells you nothing. You need a comparison.

## What it does

- Removes the direction while the model runs, leaving saved weights untouched,
  ramping from nothing to full so you can see whether refusal goes before maths.
- Checks refusal by stock phrases and by a classifier. The phrase check is
  unreliable: the paper's own appendix has them disagreeing by up to 50 points,
  because answers that warn and then help still count as refusals.
- Tests long maths (GSM8K) against short (SVAMP), plus MMLU and how far ordinary
  word predictions shift. If everything moved, nothing specific to maths was lost.
- Error bars on everything.
- Checks whether the refusal and maths directions sit near each other, against
  random directions.

## Where

One notebook, one free T4 (Colab or Kaggle), saves as it goes. Qwen2.5-1.5B,
Phi-4-mini, Granite-4.1-3B, SmolLM3-3B.

## Known problems

**Layer choice.**

**Subspace comparison.**
