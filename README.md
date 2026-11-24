# DanaShift | Applied NLP
**Multilingual customer support agent for technical consulting**

Developed as part of the **Applied Natural Language Processing Program** offered by **SDAIA Academy**, affiliated with the Saudi Data and Artificial Intelligence Authority (SDAIA).

[**Try the Live Demo**](https://danaalotaibi11.github.io/DanaShift-NLP/demo/workspace.html) · [Project Notebook](DanaShift.ipynb)

## Overview
DanaShift combines privacy-aware text preprocessing, Arabic language modeling, intent classification, entity annotation, semantic retrieval and human-supervised customer support workflows.

## Vision — From customer requests to problem resolution

DanaShift is envisioned as an intelligent, multilingual support agent that goes beyond keyword matching and ticket routing. Its long-term goal is to understand customer problems in context, reason over relevant technical knowledge, identify possible causes, recommend practical solutions, and support resolution from the initial request through follow-up.

### Future capabilities

| Capability | Intended business value |
|---|---|
| Contextual understanding of Arabic dialects and English | Understand customer intent even when requests are ambiguous or informally expressed |
| Intelligent diagnosis and troubleshooting | Identify likely causes, ask targeted follow-up questions, and recommend evidence-grounded solutions |
| Retrieval-augmented generation (RAG) | Retrieve relevant documentation, previous cases and approved procedures to support accurate answers |
| Tool-enabled problem resolution | Integrate authorized ticketing, CRM, scheduling and project systems to support appropriate actions |
| Multi-turn assistance | Maintain relevant case context and guide customers through troubleshooting and follow-up |
| Human oversight and safe escalation | Escalate critical, uncertain or sensitive cases; require approval for consequential actions |
| Privacy-aware processing | Minimize exposure of personal information throughout the support workflow |

### Development roadmap

- **Current prototype:** NLP component experiments in the project notebook and a rule-based browser demonstration of the intended workflow.
- **Next stage:** Integrate trained intent and entity models with semantic retrieval and a grounded reasoning layer; evaluate on larger multilingual datasets.
- **Future product:** Build an agent capable of contextual troubleshooting, recommending and coordinating solutions through authorized tools, with human approval where appropriate.
- **Impact validation:** Measure resolution quality, response time, routing accuracy and staff workload against a manual baseline.

The rule-based demo is a lightweight illustration of the user experience, not the intended final architecture. The future capabilities and business benefits above are development objectives, not claims of currently deployed functionality or measured outcomes.

## Experimental methodology
| Stage | Focus | Recorded result |
|---|---|---|
| 1 | Normalization, PII masking, multilingual tokenization | Arabic fertility 3.32; English 1.95; p95 length 36.5; UNK rate 0.0058 |
| 2 | Attention, masking and CAMeLBERT attention maps | PAD attention with mask 0.0; without mask 0.294 |
| 3 | CAMeLBERT classification, grouped split | Saved split: 6 train rows, 2 test rows, no shared client IDs; counts require revalidation; eval loss 3.3970 |
| 4 | BIO alignment and Arabic morphology | 8/8 alignment tests; 9/9 illustrative labels |
| 5 | MiniLM embeddings, FAISS and CrossEncoder | Example rank 2 before reranking, rank 1 after reranking |
| 6 | Sliced evaluation and error analysis | Illustrative bootstrap interval 0.375–1.0 |

These are saved notebook outputs and small exercises, not production benchmarks. The classification experiment trained four labels; automation and out-of-scope are proposed extensions. The entity annotation experiment's illustrative labels and manually specified F1 values are not measured model performance. The evaluation example uses supplied labels and predictions.

## Proposed workflow
```mermaid
flowchart TD
 A[Customer request] --> B[PII masking]
 B --> C[Intent and priority]
 C --> D[Entity extraction]
 D --> E{In scope?}
 E -->|No| H[Draft response]
 E -->|Yes| F[Knowledge retrieval]
 F --> G[Tool orchestration]
 G --> H
 H --> I[Human review]
```

## Project notebook

[**Open DanaShift.ipynb**](DanaShift.ipynb) — unified project explanation, code, saved experimental results and original Colab figures.

## Repository guide
- [Experiment notes](docs/experiments.md)
- [Interactive live demo](https://danaalotaibi11.github.io/DanaShift-NLP/demo/workspace.html) — current rule-based workflow preview; the long-term vision is a model-powered problem-resolution agent.

## Acknowledgments
SDAIA Academy, Saudi Data and Artificial Intelligence Authority, for the Applied Natural Language Processing Program.

This educational project is not an official SDAIA product. No customer messages are sent automatically.
