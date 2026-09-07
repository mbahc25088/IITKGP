# Cloud 9 — Why Forgetting Is the Price of Remembering Cheaply
**DataForge 2026 Pathway Track | Topic: Key–Value Caching, Limitations, and Alternate Approaches**

- Team: Cloud 9
- Artifact URL (Pages, no login): https://mbahc25088.github.io/IITKGP/
- Repo: https://github.com/mbahc25088/IITKGP
- Track: Pathway — Explain the Frontier

## 1. One-sentence falsifiable claim
A Transformer KV-cache allocates a new slot per token — memory grows O(n) and retrieval stays exact. A fixed-size recurrent state stays O(1) but silently forgets when writes collide.

Break test: set n=500, N=16 (Flood it). If whiteboard recall stays perfect, the claim is wrong.

## 2. Intended learner + prerequisites
2nd-year BTech who knows attention. Prereq: key→value lookup. Time: ~6 min (2 guided + 4 sandbox).

Objectives: (1) state O(n)-exact vs O(1)-lossy in own words, (2) predict n/N changes, (3) locate BDH synaptic state ρ in the trade-off, (4) name one limit (silent interference) + one misconception (BDH ≠ Mamba SSM).

## 3. Artifact architecture
Single static `index.html`, no deps, no backend, no secrets. Serif editorial + mono system stack, warm paper theme.
- `pairs(n)`: deterministic stream (`word-i` → int, FNV hash). Words: mango, river, tabla…
- Filing cabinet (KV): `Map`, one slot per token, exact. Purple cells, "+N more" overflow note.
- Whiteboard (recurrent): `slot = hash % N` + selectable rule — hash (last wins) / mamba-gate (salient kept) / delta (blend) / hola (+8 exact cache) / bdh-ρ (decay ~60 steps). Yellow=warm (overwritten), red=hot (lying to current query). Click cell → interrogate; hover → residents.
- Controls: n slider 10–500, N select 16–256, rule select (5 write/read cartoons, labeled not-real-kernels), query select. Presets: Flood it (500→16), Give it room (256), Stream (animate 20→500).
- Truth table: ground truth vs KV vs whiteboard + thief keys named.
- Charts: print-safe SVG with gridlines — slots-vs-tokens (purple climb vs amber flat), accuracy-vs-length (live recompute, 21 points) + text fallback lines.
- Quiz: 1 three-option self-check with instant feedback.
- BDH module (mid-page, not appendix): Eq.5 ρ, Hebbian framing, two evidence cards (BABILong, BDH-CQ), limitation note.
- Comparison table: Transformer vs Mamba vs HOLA vs BDH.

## 4. Role of every component
Hero claim → steps (Watch/Break/Meet BDH) → lab → bill (charts) → BDH grounding → landscape table → quiz → sources. Every control maps to a real variable (n, N, queried key). Presets/Stream are shortcuts for the same variables, not decoration.

## 5. Live / precomputed / synthetic / animated
| Part | Status |
|---|---|
| Toy memories, query, charts, quiz, Stream, 5-rule switcher | LIVE, <1s, SVG prints |
| BABILong 134M 95%@32K → 82%@128K | PRECOMPUTED vendor result, labeled pending validation |
| BDH-CQ 150M 29.5% pass@2 @ ~$0.0007 ARC-AGI-1 | PRECOMPUTED vendor result, labeled self-reported |
| Hash-%-N toy, int values, exact-match | SYNTHETIC simplification, disclosed |
| Scripted animation as model | none |

## 6. Reproduce
1. Open Pages URL (or double-click `index.html`). Starts at 120 / 32.
2. Click a yellow cell → table names thieves. Hit Flood it → recall craters, KV=500.
3. Hit Stream → watch n climb and red cells spread. Give it room → recovery.
4. Answer quiz, then verify by flooding.

## 7. Papers (2022–2026, cited beside claims)
1. Kosowski et al. Dragon Hatchling. arXiv:2509.26507 (2025) — BDH, Eqs.4–8, BDH-GPU App.E.
2. Engdahl, Kosowski et al. BDH-CQ. arXiv:2608.09888 (2026) — S_t=U(S_{t-1},D_t), Pareto $0.0007/task.
3. Cui. Hippocampus for Linear Attention. arXiv:2607.02303 (2026) — O(1)-but-lossy, overwrites.
4. Gu & Dao. Mamba (2024) — SSM baseline; BDH distinct.

## 8. Source + license record
Team-written `index.html` (MIT) with AI drafting help (Muse Spark) across code, prose, and design; team traced, tested, and defends every component. No weights/data/fonts/graphics reused. Facts via arXiv + pathway.com, linked. No forks.

## 9. AI assistance disclosure
AI drafting help (Muse Spark) used for code, prose, and design. Team traces, predicts, and defends every component. Toy labeled not-official-BDH throughout.

## 10. Limits
Hash-%-N + 4 rule cartoons ≠ learned keys/decay/sparsity or real Mamba/delta/HOLA/BDH kernels — discrete proxy for vector superposition S_t=S_{t-1}U+v_t k_t^T where q^T S_t degrades via cross-talk Σ(q^T U^{t-τ}k_τ)v_τ when n>d. Exact-match only. BDH-GPU ≠ standard linear attention (fixed φ Performer/Katharopoulos which drifts); BDH uses sparse ReLU low-rank + Hebbian + U for stability. Vendor numbers unreproduced. Forgetting silent. Session memory ≠ durable learning (fast-to-slow consolidation open).
