# LLM-Based Personalized Feedback Generator for K-12 Short-Answer Questions

A research project investigating whether **small, open-source language models** can generate meaningful, age-appropriate feedback for K-12 students (Grades 3–8) on incorrect Math/Science short-answers — without relying on large, expensive models like GPT-4.

> 📄 **Full methodology, results, and analysis are in [`NLP_Project_Paper.pdf`](./NLP_Project_Paper.pdf)** — this README only summarizes the key points.

## Authors

- Minahil Mir
- Wania Ahsan
- Abdullah Qasim

## Research Question

Can small LLMs (under 600M parameters) generate feedback good enough to help students — or do they fundamentally fail at this task? The study tests **4 model families across 11 configurations**: GPT-2 Small, Flan-T5 Small (zero-shot + fine-tuned), Flan-T5 Base, and mT5 Small — using ROUGE and BLEU metrics on a custom 100-sample dataset.

## Key Findings

- **All zero-shot models fell short of human-level feedback quality.** Flan-T5 Base with a structured, misconception-aware prompt gave the best zero-shot results (ROUGE-2: 0.0515, BLEU: 0.0183).
- **Prompt design matters a lot** — adding grade level, subject, and misconception type consistently improved output quality over basic prompts.
- **Fine-tuning gave mixed results** — Flan-T5 Small's ROUGE-1 improved by +29.4% after fine-tuning on 80 samples, but BLEU dropped −58.4%, indicating overfitting on a small dataset rather than genuine improvement.
- **mT5 Small failed completely**, producing only sentinel tokens (`<extra_id_0>`) instead of real text — incompatible with this generation task.
- Models performed better on **concrete factual errors** (e.g., gravity/force) than **abstract multi-step misconceptions** (e.g., food chain confusion).

## Dataset

A custom 100-sample dataset (Math + Science, Grades 3–8, 13 misconception categories, expert-authored feedback) was built for this study.

**Publicly available on Kaggle:** [K-12 Student Feedback Dataset](https://www.kaggle.com/datasets/hafizabdullah66/k-12-student-feedback-dataset)

## Tech Stack

Python · PyTorch · HuggingFace Transformers · HuggingFace `evaluate` (ROUGE) · NLTK (BLEU) · Google Colab (T4 GPU)

## Full Details

See [`NLP_Project_Paper.pdf`](./NLP_Project_Paper.pdf) for the complete methodology, prompt designs, fine-tuning setup, full results tables, qualitative error analysis, limitations, and future work.
