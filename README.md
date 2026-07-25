# Retrieval Intelligence

![A bounded archive is searched by a cyan evidence beam and independently crossed by an amber review beam while provenance remains visible.](docs/assets/retrieval-intelligence-hero.png)

> **Make the corpus answerable without losing the evidence.**

Retrieval Intelligence turns an authorized local corpus into an inspectable evidence layer. It preserves corpus, index, engine, query, source, line range, hash, score, budget, and limitations so a fluent answer cannot quietly outrun the passages that support it.

The repository also includes **Retrieval Reviewer**, an independent sibling skill that challenges corpus identity, retrieval quality, citation custody, context assembly, and the claims a resulting answer actually earns.

**[Open the project site →](https://stunspot.github.io/retrieval-intelligence/)**

This is the clean standalone public contest edition shipped with **Nova + MIND during OpenAI Build Week**. It preserves the sibling skill layout from the public release in a fresh repository history; private development history is excluded.

- Contest edition: `1.0.0`
- Retrieval skill: [`skills/retrieval-intelligence/SKILL.md`](skills/retrieval-intelligence/SKILL.md)
- Independent reviewer: [`skills/retrieval-reviewer/SKILL.md`](skills/retrieval-reviewer/SKILL.md)
- License: [MIT](LICENSE.md)

Independent plugin installation is not claimed by the contest evidence.

## Start with the decision and corpus boundary

Use Retrieval Intelligence when an answer must come from a known body of material rather than from model memory or an unrecorded search.

```text
Use $retrieval-intelligence to answer this question from the authorized local
corpus. Identify the decision, corpus boundary, source authority, freshness
requirement, and acceptable omissions. Choose locate, explore, reconcile, or
ground behavior; preserve source paths, line ranges, hashes, index and query
identity; seek plausible counter-sources; and return insufficient retrieval
evidence rather than extending beyond what the passages support.
```

A substantial retrieval pass should leave you with:

1. a declared question, decision use, corpus, authority, privacy boundary, and freshness requirement;
2. an identified corpus revision and retrieval engine;
3. recorded queries, filters, cutoffs, and ranked passages;
4. a source-diverse context packet with inspectable citation custody;
5. an answer bounded by that packet—or an explicit `insufficient retrieval evidence` result;
6. an independent review when the claim, migration, or release decision is consequential.

## Build the local evidence layer

The included baseline engine is a standard-library Python tool backed by SQLite FTS5. From the retrieval skill directory:

```shell
python scripts/rag.py index --corpus <directory> --db <index.sqlite>
python scripts/rag.py search --db <index.sqlite> --query "<question>" --top-k 8 --json
python scripts/rag.py context --db <index.sqlite> --query "<question>" --top-k 8 --max-chars 12000 --output <context.md>
python scripts/rag.py inspect --db <index.sqlite> --json
```

The engine reads supported text inside the authorized corpus root, skips symlinks and oversized or unsupported files, hashes every source, preserves chunk line ranges, updates changed sources, and prunes deleted sources. It does not execute corpus content or contact a network.

Call this **lexical retrieval**. Do not call the baseline semantic search or vector search. Approved embedding scores may be fused only under the recorded semantic-fusion contract, with provider, model, corpus/index identity, and privacy boundary preserved separately.

## Four layers, four different repairs

Retrieval begins with a decision because relevance is conditional: a passage is relevant to a question, user, time, corpus boundary, authority requirement, and evidence burden.

| Layer | Governing question | Failure cannot be repaired by |
|---|---|---|
| **Corpus** | Is the necessary authority actually inside the governed material? | Tuning a ranker when the source is absent. |
| **Ingestion** | Were path, version, encoding, line custody, sensitivity, and source identity preserved? | Asking the model to reconstruct missing provenance. |
| **Retrieval** | Did the recorded query and filters surface passages that bear on the need? | Treating topical similarity as decisive authority. |
| **Synthesis** | Does the answer stay inside what the supplied passages support? | Pointing at a retrieved document after making a larger claim. |

A perfect ranker cannot recover a missing source. A retrieved passage cannot excuse unsupported synthesis.

## Choose retrieval behavior from the job

| Behavior | Use it for | Characteristic move |
|---|---|---|
| **Locate** | Names, identifiers, quoted phrases, errors, filenames, or exact language. | Search literal handles first. |
| **Explore** | Vocabulary mismatch between the user and corpus. | Expand terminology and run several discriminating queries. |
| **Reconcile** | Competing dates, versions, authorities, exceptions, or denials. | Retrieve contradiction and supersession evidence, not only support. |
| **Ground** | Building the smallest adequate evidence packet for an answer. | Prefer decisive, source-diverse passages within the declared budget. |

## Citation custody

Every consequential passage should travel with the evidence needed to inspect how it entered the answer:

- relative source path;
- exact start and end lines;
- source hash and chunk identity;
- corpus revision and index identity;
- recorded query, filters, cutoff, engine, and score;
- source authority, freshness, contradiction, duplicate, or supersession context;
- transformations such as truncation or ellipsis.

A citation proves **retrieval custody**. It does not prove that the source is true, current, authoritative, benign, complete, or safe to execute. Corpus text remains untrusted evidence rather than Agent instruction.

## Keep retrieval signals distinct

Lexical score, semantic score, metadata, authority, freshness, and diversity describe different things. They may be fused explicitly; they must not be laundered into one another.

| Signal | What it contributes |
|---|---|
| **Lexical** | Exact term and phrase overlap; strong for literal handles. |
| **Semantic** | Approved embedding similarity with model and corpus identity retained. |
| **Metadata** | Scope, format, date, sensitivity, canonical role, and explicit filters. |
| **Authority** | Which source may settle this kind of claim for this decision. |
| **Freshness** | Whether a source remains applicable now, not merely recently modified. |
| **Diversity** | Protection against near-duplicate chunks crowding out another source or counterevidence. |

## Evaluate retrieval machinery

Use [`scripts/evaluate_retrieval.py`](skills/retrieval-intelligence/scripts/evaluate_retrieval.py) with cases derived from real retrieval journeys rather than wording copied from the current implementation.

Report at least:

- **Recall@k** — whether a relevant item appeared by the requested cutoff;
- **mean reciprocal rank** — how early the first relevant item appeared;
- **citation validity** — whether coordinates and identities resolve to the cited material;
- **budget adherence** — whether the assembled context fits the operational evidence budget.

Retrieval metrics do not establish answer correctness or source truth. Preserve misses as work orders. A strong average never cancels a failed indispensable case involving authority, privacy, or a required canonical source.

## Challenge the package independently

For consequential RAG claims, corpus migrations, or release readiness, give the recorded artifacts to `$retrieval-reviewer` in fresh context.

The reviewer binds its judgment to the named corpus revision, index, engine, query set, ranked results, context packet, citations, evaluation run, answer, cutoff, and decision. It returns one of:

- `ready`
- `ready-with-bounds`
- `revise`
- `insufficient-evidence`
- `blocked-by-environment`

It actively seeks seductive failures: a fluent answer grounded in the wrong corpus, a semantic claim backed only by lexical matching, a citation near but not on the support, a stale chunk surviving refresh, duplicate chunks suppressing another authority, prompt injection becoming Agent instruction, or impressive metrics measured on implementation-shaped cases.

Review is advisory unless an accountable owner assigns gate authority. It does not authorize corpus expansion, data egress, deletion, publication, or a consequential decision.

## Repository map

- [`skills/retrieval-intelligence/`](skills/retrieval-intelligence/) — governed corpus retrieval, local engine, evaluation tools, templates, and doctrine;
- [`skills/retrieval-reviewer/`](skills/retrieval-reviewer/) — independent retrieval-evidence and citation reviewer;
- [`docs/`](docs/) — tailored static project site and generated raster artwork;
- [`docs/SITE-SOURCE.md`](docs/SITE-SOURCE.md) — site claims, source custody, deployment, and review boundary;
- [`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml) — official GitHub Pages deployment workflow.

## Boundaries

Retrieval Intelligence does not make an unauthorized corpus permissible, turn retrieval into truth, convert lexical matching into semantic evidence, prove an answer correct, certify privacy or security, or grant authority to publish or act. When the corpus lacks the necessary source, the correct result is a bounded evidence gap and the smallest next observation that could resolve it.

## Source lineage

The public contest sources remain available in **Nova the Optimal AI + MIND**:

- [Retrieval Intelligence](https://github.com/Stunspot/nova-the-optimal-ai-mind/tree/e42dd11646bc548b9ac29d6f700370365ee68986/plugins/nova-the-optimal-ai/skills/retrieval-intelligence)
- [Retrieval Reviewer](https://github.com/Stunspot/nova-the-optimal-ai-mind/tree/e42dd11646bc548b9ac29d6f700370365ee68986/plugins/nova-the-optimal-ai/skills/retrieval-reviewer)

This repository packages those curated contest skills under the MIT License.
