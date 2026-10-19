# Hybrid retrieval data (three public CDC guidelines)

Experiment files for the MLNLP 2026 paper **Hybrid Retrieval as the Speed-Accuracy Trade-off on Three Public Clinical Guidelines**.

One frozen 540-chunk index. Three retrievers on the same 127 questions: dense (`bge-small-en-v1.5` + FAISS), hybrid (dense + BM25, RRF), and hybrid + `bge-reranker-base`. Retrieval ran locally on an RTX 4060 Laptop GPU. Questions were written by DeepSeek-Flash from the source chunks (not clinician-authored).

## Layout

| Path | What it is |
| --- | --- |
| `data/raw/` | Three CDC PDFs (public domain) |
| `data/processed/chunks.jsonl` | 540 chunks |
| `data/processed/dataset.jsonl` | 127 questions and gold chunks |
| `data/index/` | FAISS vectors, BM25 tokens, chunk store |
| `data/results/paper/retrieval_summary.csv` | Table I |
| `data/results/paper/paired_deltas.csv` | Table II |
| `data/results/paper/reranker_pool.csv` | Table III (pool of 20) |
| `data/results/paper/per_query_retrieval.csv` | Per-question ranks and latency |
| `data/results/paper/figures/` | Paper figures |
| `configs/experiment.yaml` | Frozen run settings |
| `DATA_SOURCES.md` | PDF URLs, SHA-256, page/chunk counts |

Do not rebuild the index or retime retrieval if the goal is to match the paper tables.

## Metrics

Binary gold-chunk hit. Recall@5, MRR = 1/r, nDCG@5 = 1/log2(r+1). Bootstrap: 1000 resamples of 127 paired differences, seed 20261001.

## License

CDC PDFs are U.S. government works (17 U.S.C. § 105), public domain. Retrieval scores, questions, and figures in this repo are released for reproducing the paper.
