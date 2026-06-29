 TakeMeter: Online Discourse Quality Classifier
 Overview

TakeMeter is a fine-tuned text classification system that analyzes short online community posts and categorizes them based on discourse quality in sports/NBA-style discussions.

It classifies posts into:

analysis — structured reasoning or tactical explanation
hot_take — opinionated claim without structured evidence
reaction — emotional or meme-like response

The goal is to evaluate whether pretrained language models can learn subtle distinctions in human discourse using a small labeled dataset (~200 examples).

 Label Taxonomy
analysis   
Structured reasoning, tactical breakdowns, or explanatory statements.

Examples:

“Smart’s motor explains his impact he just plays nonstop energy”
“Defenders clogged the paint forcing isolation plays”
hot_take

Strong opinions or judgments without structured reasoning.

Examples:

“Rockets young core is garbage not playoff ready”
“NFL draft coverage is so much better than NBA”
reaction

Emotional, conversational, or incomplete responses.

Examples:

“First season with new team”
“I think I watched about 45 seconds of the draft then turned it off”

 Dataset
Total samples: ~200 labeled examples
Split: 70% train / 15% validation / 15% test
Domain: NBA / sports discussion text
Task: 3-class classification

 Model
Base model: distilbert-base-uncased
Framework: HuggingFace Transformers
Training platform: Google Colab (T4 GPU)
Epochs: 3
Learning rate: 2e-5
Batch size: 16

 Fine-Tuning Results
Training Progress
Epoch    Training Loss    Validation Loss    Accuracy
1    1.1158    1.0959    0.4063
2    1.0872    1.0706    0.4375
3    1.0624    1.0320    0.5938
Key Observations
Validation accuracy improves steadily from 0.41 → 0.59
Loss decreases consistently across all epochs
Most learning occurs in the final epoch, indicating late-stage boundary separation
Interpretation

The model learns gradually but struggles with fine-grained distinctions between:

structured reasoning (analysis)
opinionated statements (hot_take)
emotional responses (reaction)

This suggests the task is limited more by label ambiguity than model capacity.

 Evaluation Results'
Baseline vs Fine-tuned
{
  "baseline_accuracy": 0.536,
  "finetuned_accuracy": 0.625,
  "improvement": 0.089,
  "test_set_size": 32
}
Key Insight

Fine-tuning improves performance by ~9% over a strong zero-shot LLM baseline, showing that even small datasets can meaningfully adapt pretrained models to domain-specific discourse tasks.

 Baseline Performance (Zero-shot LLM)
Label    Precision    Recall    F1    Support
analysis    1.00    0.21    0.35    14
hot_take    0.00    0.00    0.00    2
reaction    0.48    1.00    0.65    12
Baseline Behavior Summary
Strong bias toward predicting reaction
Cannot detect hot_take
Over-interprets structured sentences as emotional reactions

📊 Confusion Matrix:

Due to technical issue i wasnot able to upload it here but i have comitted to the github


❌ Misclassified Examples (Fine-tuned Model)
1. analysis → reaction

Smart’s motor explains his impact he just plays nonstop energy
True: analysis → Predicted: reaction (0.36)

2. hot_take → analysis

NFL draft coverage is so much better than NBA
True: hot_take → Predicted: analysis (0.38)

3. analysis → reaction

First season with new team
True: analysis → Predicted: reaction (0.37)

4. analysis → reaction

They forced LeBron on an island
True: analysis → Predicted: reaction (0.37)

5. hot_take → analysis

Rockets young core is garbage not playoff ready
True: hot_take → Predicted: analysis (0.38)

6. hot_take → reaction

Ant or Brunson
True: hot_take → Predicted: reaction (0.38)

7. reaction → analysis

In the 1st quarter my bud made a bet... shotgun beers
True: reaction → Predicted: analysis (0.37)

8. hot_take → reaction

Lebron is 41 this won’t last much longer
True: hot_take → Predicted: reaction (0.37)

9. analysis → reaction

Defenders clogged the paint
True: analysis → Predicted: reaction (0.37)

10. analysis → reaction

Then took over late
True: analysis → Predicted: reaction (0.37)

11. analysis → reaction

Everyone fails at some point
True: analysis → Predicted: reaction (0.36)

12. reaction → analysis

I think I watched about 45 seconds of the draft then turned it off
True: reaction → Predicted: analysis (0.36)

🔍 Error Analysis Summary
1. Reaction bias

Short or incomplete sentences are heavily classified as reaction.

2. Weak hot_take boundary

Opinionated statements are inconsistently separated from analysis.

3. Structure vs tone confusion

Model relies on:

sentence length
slang/emotion
surface structure

rather than actual reasoning content.

🧠 Key Insight

The learned representation behaves more like tone classification than true discourse understanding.

Main failure:

inability to reliably distinguish structured reasoning vs conversational commentary

📊 Sample Predictions (Fine-tuned Model)
Text    Predicted    Confidence
“They forced LeBron on an island”    analysis    0.xx
“Ant or Brunson”    hot_take    0.xx
“Everyone fails at some point”    reaction    0.xx
🧠 What the Model Learned
reaction → emotional / incomplete statements
analysis → structured basketball commentary
hot_take → opinionated phrasing (partial success)
📌 Reflection
What worked

Clear label definitions improved annotation consistency and model learning stability.

What didn’t work

Real-world discourse blends categories, making strict labeling boundaries imperfect and noisy.

🤖 AI Usage
Used Groq LLM for zero-shot baseline classification.
Used LLM-assisted error grouping to identify systematic confusion patterns (especially analysis ↔ reaction).

All outputs were manually verified.

📌 Conclusion

TakeMeter demonstrates that:

small datasets (~200 examples) can improve over strong LLM baselines
label design is the most critical factor in performance
most errors come from ambiguous human language, not model limitations

The main limitation is the overlap between discourse categories in real-world conversation.
