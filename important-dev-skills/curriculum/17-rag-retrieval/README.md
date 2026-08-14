# Module 17: RAG and retrieval

## Outcome

Build and evaluate a retrieval pipeline that can distinguish missing evidence from generation failure.

## Lab progression

1. Create a small approved document corpus and answerable question set.
2. Establish lexical and vector-search baselines.
3. Experiment with chunk boundaries, overlap, and document structure.
4. Add metadata filters for access, version, source, and date.
5. Combine lexical and semantic retrieval where the corpus supports it.
6. Add reranking and measure whether it improves relevant-context placement.
7. Require answers to cite retrieved evidence and abstain when support is absent.
8. Test stale, conflicting, inaccessible, and adversarial documents.

## Required evidence

- A versioned corpus and query/relevance judgments.
- Retrieval metrics such as recall at a chosen cutoff, reported separately from answer quality.
- Ablation results for chunking, filtering, hybrid search, or reranking choices.
- Examples of retrieval miss, generation miss, and correct abstention.

## Pass conditions

- Access filtering happens before restricted content reaches generation.
- Retrieval and answer evaluation remain separate.
- Citations map to actual source passages.
- Missing evidence produces an explicit abstention or limitation.
- Corpus and index version are traceable for every evaluated run.
