# Module 17: Retrieval-augmented generation (RAG)

## Start here

You will build a tiny local policy corpus, search it with standard-library methods, apply access/version/date filters, measure Recall@k, and map citations to real passages. The corpus is synthetic and no embedding or model service is called.

Prerequisite: [Module 16](../16-tool-calling-agent-architecture/README.md), especially contracts, authorization, and untrusted text. This module introduces basic measurement of retrieval results; formal AI evaluation is introduced in [Module 18](../18-ai-observability-evaluation/README.md). Read [LESSON.md](LESSON.md) before [lab.ipynb](lab.ipynb).

## Learning goals

- explain documents, chunks, embeddings, lexical search, similarity, metadata, and reranking;
- keep retrieval quality separate from answer-generation quality;
- filter access, version, and effective date before context construction;
- calculate Recall@k and run a chunking experiment;
- require citation-to-passage mapping and explicit abstention;
- recognize retrieval misses, generation misses, stale evidence, and prompt injection.

## Vocabulary preview

The [lesson](LESSON.md) introduces each retrieval idea with synthetic examples:

- **Document:** a source record such as a policy page.
- **Chunk:** a bounded piece of a document used for search or context.
- **Retrieval:** finding candidate passages relevant to a query.
- **Metadata:** fields such as version, access group, and effective date.
- **Filter:** a rule that removes ineligible results before context construction.
- **Recall@k:** the fraction of judged relevant passages found in the first k results.
- **Abstention:** explicitly saying the available evidence is insufficient.

## Study order (90–150 minutes)

Read the lesson (45–60 min), run the corpus/index experiments and predictions (45–65 min), then complete the independent challenge and evidence handoff (10–20 min).

## Completion checklist

- [ ] I can distinguish a retrieval miss from a generation miss.
- [ ] Access and freshness filters run before context reaches an answerer.
- [ ] Every citation maps to a retrieved passage, not just an invented ID.
- [ ] I measured Recall@k and recorded corpus/index/query versions.
- [ ] No-evidence and adversarial passages produce safe abstention or limitation.

## Evidence and pass conditions

Keep the versioned synthetic corpus, metadata policy, query judgments, raw ranked results, Recall@k and latency, filter tests, citation mapping, abstention examples, AI review, and ablation decision. Pass means restricted/stale text never reaches context, retrieval and generation are scored separately, citations are real, and insufficient evidence is explicit. This toy lexical/vector-like search cannot prove large-corpus quality.

## Next module

Finish with [Module 18: AI observability and evaluation](../18-ai-observability-evaluation/README.md).
