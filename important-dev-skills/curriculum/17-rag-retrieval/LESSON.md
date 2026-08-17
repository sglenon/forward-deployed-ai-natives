# Retrieval before generation

## What you will learn

You will construct a small policy search pipeline and learn why a fluent answer is not evidence. The lesson uses local synthetic documents, but the concepts apply to a larger retrieval-augmented generation system.

## Vocabulary

- **Document:** a source record, such as a policy page.
- **Chunk:** a bounded piece of a document sent to search or context.
- **Corpus:** the collection of documents.
- **Index:** a structure that makes lookup faster.
- **Lexical search:** matching words or terms.
- **Embedding:** a numeric representation intended to place similar meanings near each other.
- **Similarity:** a score describing how close a query and passage are.
- **Metadata:** descriptive fields such as owner, version, group, and effective date.
- **Filter:** a rule that removes ineligible results.
- **Rerank:** reorder an initial result set using a second scoring rule.
- **Recall@k:** the fraction of known relevant items found in the first k results.
- **Citation:** a pointer from a claim to a specific source passage.
- **Abstention:** explicitly saying evidence is insufficient rather than guessing.
- **Retrieval miss:** the relevant passage was not returned.
- **Generation miss:** the relevant passage was returned but the answer is wrong or unsupported.
- **Prompt injection:** untrusted source text that tries to override instructions.

## Why retrieval and generation are separate

An answerer cannot use evidence it never received. If the right policy is ranked 20th and you pass only three passages, changing the prompt may not help. Conversely, if the right passage is present but the answer invents a date, retrieval succeeded and generation failed. Measure the stages independently.

## Mental model: collect → filter → rank → cite

```text
corpus → chunk/index → candidate search → access/version/date filters
       → rank/rerank → bounded context → answer claims + citations/abstain
```

Filters belong before context construction. Returning a restricted passage and hoping the prompt ignores it is a leak. Metadata travels with each chunk so later stages can explain why a passage was eligible.

## Chunks and metadata

A chunk should be small enough to search and quote, but large enough to preserve meaning. Preserve document ID, section, version, access group, effective date, and chunk text. Cutting in the middle of a rule can turn “not allowed unless…” into misleading evidence. Compare bounded chunk sizes rather than tuning until one query looks good.

## Lexical and vector-like search

Lexical search counts shared normalized words. It is transparent but misses synonyms. A real embedding maps text to vectors; similarity might use cosine similarity. The notebook uses `collections.Counter` and a simple overlap score as a deterministic vector-like teaching aid, not a production embedding. A hybrid search combines lexical and semantic signals; reranking can use metadata and a more precise score on a small candidate set.

## Measuring Recall@k

For a query with judged relevant passage IDs, Recall@k is:

```text
number of relevant IDs in top k / number of relevant IDs in the corpus
```

Define judgments before running. Report query count, k, corpus/index version, rank, and latency. Recall can hide ordering, unauthorized results, stale versions, and answer quality; it is one signal, not a release decision.

### A worked metric example

Imagine a query whose judged relevant passage IDs are `{p1, p7}`. If the top three results are `[p4, p1, p9]`, one of the two relevant IDs was found, so Recall@3 is `1 / 2 = 0.5`. If the top three are `[p7, p1, p4]`, Recall@3 is `2 / 2 = 1.0`. The metric does not say whether p7 was first, whether p4 was authorized, or whether an answerer quoted the passage correctly. Record the denominator and the query's slice so a reviewer can interpret the number.

A tiny test set is useful for learning but unstable as a product estimate. One query moving from a miss to a hit changes the rate dramatically. Add more representative queries, preserve fixed relevance judgments, and report counts before claiming an improvement. Do not change the judgments after seeing a candidate ranking; that would measure agreement with a moving target.

## Access, freshness, and conflicts

A user/group filter is authorization. Version and effective-date filters are correctness constraints. Apply all three before generation. If two versions conflict, state the policy: choose the document effective for the requested date, or abstain when equal dates conflict. Never cite an inaccessible document just because its words match.

### Why filtering order matters

Consider an inaccessible passage that contains the exact answer. If search ranks it first and the system builds context before checking the group, the model has already received restricted text. Removing it from the final answer does not undo the disclosure; the text may appear in logs, prompts, or a citation. The safe order is:

```text
candidate documents → access check → effective-date/version check
                     → score/rerank eligible chunks → build context
```

Filtering can happen before lexical scoring or immediately after a bounded candidate search, but it must happen before context and citations. Keep the policy decision visible in a test: an all-user query excludes a contractors-only record, while a contractor query may include it. A stale record should likewise be absent for a date after a newer effective policy when the product chooses the newest applicable version.

## Citations and abstention

Store a citation mapping from answer claim to retrieved chunk ID and section. Validate that every cited ID is actually in the retrieved set and that text matches the stored passage. If no eligible passage crosses a threshold, return an explicit limitation such as “I could not find an applicable policy.” A made-up citation is worse than no answer.

## Failure taxonomy and AI review

Label each failure as retrieval miss, generation miss, policy/access failure, stale/conflict data, or citation failure. AI-generated retrieval code often applies filters after context assembly, returns unbounded results, drops metadata during chunking, or computes Recall with the answer text instead of judged passages. Ask for a small diagnostic diff, verify ranking and filter behavior, and reject aggregate improvements that expose restricted content.

## Common mistakes

- Calling a fluent answer proof that retrieval succeeded.
- Filtering after generation instead of before context.
- Citing a document ID without a passage/section mapping.
- Treating a toy overlap score as a semantic embedding.
- Tuning chunk size on one query and claiming general improvement.
- Including adversarial source text as trusted instructions.

## Knowledge checks

1. What observation distinguishes retrieval from generation failure?
2. Where must access filtering happen?
3. What does Recall@k measure and hide?
4. Why preserve metadata on every chunk?
5. When should an assistant abstain?

### Answers

1. Inspect ranked passages before reading the answer: absent evidence is a retrieval miss; present evidence with a wrong claim is generation miss.
2. Before context reaches generation or citation selection.
3. It measures judged relevant passage coverage in top k; it hides rank quality, authorization, freshness, and answer correctness.
4. Filters, citations, and reproducibility need source identity, section, version, and policy fields.
5. When no eligible passage provides enough evidence, or conflicts cannot be resolved safely.

## Notebook preparation

Run [lab.ipynb](lab.ipynb) from a fresh Python 3 kernel. The notebook creates five synthetic policy records, uses Counters/math only, and writes nothing. Keep raw rankings and metric output.

## Summary and next connection

RAG quality is a chain: eligible evidence must be retrieved, ranked, passed safely, and cited accurately. Measure each link. Module 18 closes the course by versioning traces and evaluations so changes can be released based on evidence rather than feel.
