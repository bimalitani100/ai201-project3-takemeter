> **Skeleton.** Every section below is required by the submission checklist. Fill each with real content as you finish the milestones — this is your final report, written for someone who hasn't read your planning.md. Do not leave a section as a placeholder at submission. Nothing here invents results; the numbers come from your own Colab run.

# TakeMeter

**[FILL IN]** 1–2 sentence summary: what this is (a fine-tuned classifier for discourse quality on r/nba) and the three labels.

## Community choice & reasoning
**[FILL IN]** Which community and why; what makes its discourse varied enough to classify. (Pull from planning.md §1, in your own words.)

## Label taxonomy
**[FILL IN]** Each label defined in one sentence, with **2 example comments per label**.

## Dataset
**[FILL IN]**
- Where you collected the data (which threads/sort orders).
- Your labeling process and your inclusion rule (what counted as a take vs. skip).
- **Label distribution** — a count-per-label table.
- **3 difficult-to-label examples** and what you decided for each.

## Fine-tuning approach
**[FILL IN]** Base model (`distilbert-base-uncased` or your choice), the training setup, and **at least one hyperparameter decision** you made and why (learning rate / epochs / batch size).

## Baseline
**[FILL IN]** The exact Groq `llama-3.3-70b-versatile` classification prompt you used, and how you collected its results on the locked test set.

## Evaluation report

### Overall accuracy (both models)
**[FILL IN]** Fine-tuned vs. zero-shot baseline on the same test set.

### Per-class metrics (both models)
**[FILL IN]** Precision / recall / F1 per label, for both models.

### Confusion matrix (fine-tuned model)
**[FILL IN]** Write it out as a **markdown table** here (rows = true label, columns = predicted). Keep the committed `confusion_matrix.png` as a supplementary copy, but this text table is the one that's graded.

|              | pred: analysis | pred: hot_take | pred: reaction |
|--------------|----------------|----------------|----------------|
| true: analysis |  |  |  |
| true: hot_take |  |  |  |
| true: reaction |  |  |  |

### Wrong predictions analyzed
**[FILL IN]** At least **3 specific misclassifications**, each with analysis: which labels were confused, why that boundary is hard, whether it's a labeling problem or a data problem, and what would fix it.

### Sample classifications
**[FILL IN]** A table of **3–5 posts** run through your fine-tuned model, each with predicted label and **confidence score**. For at least one correct prediction, add a sentence on why it's reasonable.

| comment | predicted label | confidence | note |
|---------|-----------------|-----------|------|
|  |  |  |  |

## Reflection: what the model learned vs. what I intended
**[FILL IN]** A higher-level observation about the gap between your label definitions and what the model's decision boundary actually captured — what it overfit to, what it missed. (Distinct from listing wrong predictions.)

## Spec reflection
**[FILL IN]** One way the spec helped guide your implementation, and one way your implementation diverged from it and why.

## AI usage
**[FILL IN — at least 2 specific instances.]** What you directed an AI tool to do, what it produced, and what you changed or overrode. Disclose any annotation assistance.
- *Pre-seed (confirm/edit for accuracy):* Claude helped draft the structure and the data-collection/metrics sections of planning.md, and ran a label stress-test (planning.md Appendix A) that I reviewed and used to tighten my definitions.
- **[FILL IN]** Second instance (e.g., failure-pattern analysis, or LLM pre-labeling during annotation).

## How to run
**[FILL IN]** If you built the optional deployed interface, document how to run it. Otherwise note how to reproduce the notebook run.
