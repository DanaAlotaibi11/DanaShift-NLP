# Experimental record

The supplied notebooks are the source of the following observations. No experiments were rerun for this documentation.

## Lab 1 — preprocessing
Multilingual DistilBERT tokenization on six examples. Fertility (subwords per word): Arabic 3.32, English 1.95. p95 length 36.5; unknown token fraction 0.0058. The masking exercise leaves some example identifiers visible, so it needs additional validation before deployment.

## Lab 2 — transformer attention
Random Q/K/V and multi-head attention illustrate mechanics; they do not establish learned relevance. A causal mask illustrates autoregressive access. CAMeLBERT attention maps show pretrained attention. PAD leak exercise: 0.0 masked versus 0.294 unmasked.

## Lab 3 — intent classification
CAMeLBERT-mix, four classes (cloud, meetings, proposals, security), 16 examples, client-group split (6 train clients, 2 test clients, zero overlap). Eight epochs, batch size 2, learning rate 3e-5. Recorded evaluation loss 3.3970224857330322. No checkpoint supplied; no claim of production accuracy.

## Lab 4 — entity alignment and Arabic processing
BIO tagging and subword alignment: 8/8 alignment checks. One illustrative label comparison: 9/9. The printed 0.82 and 0.88 macro-F1 values were manually specified, not calculated from predictions.

## Lab 5 — retrieval
Five indexed texts; semantic search using SentenceTransformer and FAISS. One example's relevant result was ranked second in the separately supplied ranking exercise (Recall@10 1; MRR@10 0.5). CrossEncoder reranking moved the relevant incident to first place.

## Lab 6 — evaluation
Language, dialect and length slices; bootstrap interval 0.375–1.0 on supplied arrays of eight examples. Error examples include proposal versus automation and cloud versus security. This is an exercise, not a measured end-to-end benchmark.

## Next steps
Expand labeled datasets, export trained checkpoints, evaluate on held-out customers, add real knowledge documents, validate privacy masking and tool adapters. Never publish actual customer identifiers.
