# ADR-001: Use of BERT and NLP for Short-Answer Scoring

## 1. Context

The SoftArchCert AI-Powered Certification System requires an automated grading solution for short-answer responses. Manual grading is time-consuming and not scalable, especially with the expected 5-10× increase in certification requests.

To ensure accurate, fair, and scalable grading, we considered multiple AI-driven approaches for Natural Language Processing (NLP)-based assessment. The key requirements for the solution are:
-	Understand meaning beyond keywords (semantic analysis).
-	Provide partial credit for near-correct answers.
-	Generate feedback explaining the score.
-	Continuously improve with expert-reviewed corrections.

After evaluating several NLP-based models, BERT (Bidirectional Encoder Representations from Transformers) emerged as the best choice due to its context-aware text understanding and adaptability to grading tasks.

## 2. Decision

We decided to use BERT-based NLP models for automated short-answer grading for the following reasons:

Advantages of BERT for Short-Answer Scoring
1.	Semantic Understanding
-	Unlike traditional keyword-based approaches, BERT captures context and understands meaning even if phrasing varies.
-	Example:
	-	“Cloud computing allows on-demand access to resources.”
	-	“Computing in the cloud provides scalable resources when needed.”
	-	BERT understands that both answers mean the same thing.
2.	Handles Synonyms & Paraphrasing
-	BERT is pre-trained on a vast corpus, making it robust to different ways of expressing the same concept.
-	Traditional models (TF-IDF, bag-of-words) fail when answers are structurally different but semantically similar.
3.	Partial Credit Assignment
-	By computing cosine similarity between the candidate’s answer and the reference answer, BERT enables partial scoring.
-	Example Scoring:
	-	“AI models learn from large datasets.” → 100% correct
	-	“Machine learning models need data to train.” → 80% correct
	-	“AI is a program that thinks.” → 30% correct (too vague)
4.	Feedback & Explainability
-	By leveraging knowledge graphs and attention mechanisms, BERT can provide justifications for scores.
-	Example feedback:
	-	“Your answer missed the key idea of ‘on-demand resource provisioning’.”
5.	Fine-Tuning on Expert-Graded Data
-	We can continuously retrain BERT on real-world responses reviewed by human experts.
-	The model adapts to grading patterns over time.
6.	Scalability & Performance
-	BERT enables batch processing, fast inference, and real-time grading.
-	Can be deployed on GPU/TPU servers or optimized for edge inference.

## 3. Alternatives Considered

| Approach | Pros | Cons |
| --- | --- | --- |
| **TF-IDF + Rule-Based Scoring** | Simple to implement, fast | Cannot understand context, fails with synonyms |
| **LSTM-based NLP Model** | Understands sequences, lightweight | Weaker than BERT for long text, needs large training data |
| **GPT (Generative Pretrained Transformer)** | Can generate detailed feedback | Computationally expensive, harder to fine-tune for grading |
| **Human-only Grading** | High accuracy, full feedback | Not scalable, expensive, slow turnaround |

## 4. Decision Outcome
-	BERT will be used as the core NLP model for short-answer grading.
-	Fine-tuning will be performed on expert-reviewed responses to improve accuracy.
-	A hybrid approach will be used:
	-	AI auto-grades most answers.
	-	Flagged responses go through manual expert review.
	-	A retraining pipeline will be implemented to continuously improve model performance.

## 5. Risks & Mitigations

| Risk | Mitigation Strategy |
| --- | --- |
| AI might misinterpret ambiguous answers | Use confidence scoring to flag uncertain cases for expert review
| Model could be biased due to training data | Regular audits with human-in-the-loop oversight |
| Computational cost of BERT | Optimize using distilled BERT for faster inference |

## 6. Status

Accepted – Implementing BERT as the core NLP model for short-answer scoring.

## 7. Next Steps
-	Fine-tune BERT on expert-labeled data.
-	Implement a feedback system for AI-explained scores.