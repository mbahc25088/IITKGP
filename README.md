[Uploading README.md…]()
# Cloud 9 — KV-Cache Grows, Recurrent State Forgets
**DataForge 2026 Pathway Track | Topic: Key–Value Caching, Limitations, and Alternate Approaches**

- Team: Cloud 9
- Artifact URL (Pages, no login): https://mbahc25088.github.io/IITKGP/
- Repo: https://github.com/mbahc25088/IITKGP
- Track: Pathway — Explain the Frontier

## 1. One-sentence falsifiable claim
A Transformer KV-cache allocates a new slot per token — memory grows O(n) and retrieval stays exact. A fixed-size recurrent state stays O(1) but silently forgets through interference when writes collide.

If the artifact cannot show recurrent accuracy dropping as n ≫ N while KV stays 100%, the claim is wrong.

## 2. Intended learner + prerequisites
2nd-year BTech who knows what attention is. Prereq: key→value lookup. Time: ~5 min guided + sandbox.

Learning objectives: (1) explain O(n) vs O(1) trade-off in own words, (2) predict what raising n or shrinking N does, (3) locate BDH's synaptic state in this trade-off, (4) name one limitation + one misconception (BDH ≠ Mamba SSM).

## 3. Architecture of artifact
Single static `index.html`, vanilla JS + Canvas, no deps, no backend, no credentials.
- `pairs(n)`: toy key→value stream (`word-i` → int), deterministic hash.
- KV side: `Map`, grows per token, always exact. Bar capped at 120 shown + "+N more" label.
- Recurrent side: array of N slots, `slot = hash(key) % N`, overwrite on collision. Yellow = overwritten, red = queried slot.
- Query panel: ground truth vs KV vs recurrent + thief keys.
- Charts: memory-slots-vs-tokens (purple growing vs green flat), recall-vs-length (live compute).
- BDH module (Section 3): Eq.5 rho, Hebbian framing, precomputed BABILong + BDH-CQ points.

## 4. Role of every major component
Every chart/control serves the claim. Sequence slider → n. Slot select → N. Query select → visible collision. Charts → cost of exactness. BDH section → real-architecture grounding.

## 5. Live / precomputed / synthetic / animated
| Part | Status |
|---|---|
| Toy memories, query table, both charts (small n) | LIVE in browser, <1s |
| BABILong 134M 95%@32K, 82%@128K | PRECOMPUTED vendor result, labeled, pending validation |
| BDH-CQ 150M 29.5% pass@2 @ $0.0007 ARC-AGI-1 | PRECOMPUTED vendor result, labeled self-reported |
| Toy hash/modulo, int values | SYNTHETIC simplification, disclosed |
| No scripted animation passed as model | none |

## 6. How to reproduce
1. Open https://mbahc25088.github.io/IITKGP/ (or double-click `index.html`).
2. Default 120 pairs / N=32 already running. Find a red row → note thief keys.
3. Drag length to 500 → recurrent accuracy falls, KV stays 100%, purple line grows, green flat.
4. Set N=16 vs 256 → collisions rise/fall. All <1s.

## 7. Papers cited beside claims (all 2022–2026)
1. Kosowski et al. The Dragon Hatchling. arXiv:2509.26507 (2025) — BDH architecture, Eqs.4–8, BDH-GPU code App.E.
2. Engdahl, Kosowski et al. BDH-CQ. arXiv:2608.09888 (2026) — S_t=U(S_{t-1},D_t), no eval demos in training, no weight update at inference, Pareto point.
3. Cui. A Hippocampus for Linear Attention. arXiv:2607.02303 (2026) — O(1) but lossy, overwrites, needle recall degrades. Independent claim match.
4. Gu & Dao. Mamba (2024) — SSM baseline; BDH distinct, do not conflate.

## 8. Source + license record
Code: team-written `index.html` (MIT). No weights, data, fonts, graphics reused. Paper factsvia arXiv/pathway.com, linked. No forked components.

## 9. AI assistance disclosure
AI-assisted coding/writing/design used (Muse Spark via OpenCode). Team understands, traced, and defends every component. No undisclosed fork. Toy is labeled not-official-BDH.

## 10. Known limitations
Hash-modulo ≠ learned keys/decay/sparsity. Exact-match queries only. BABILong/ARC numbers are vendor-reported, not independent reproductions. Fixed-state forgetting is silent. Within-session ≠ durable cross-session learning.
