# One-page concept summary — The Price of Remembering Cheaply (Cloud 9, ~730 words)

Transformers remember by keeping everything. Each token's key and value vectors stay in a KV-cache, so memory grows O(n) and any past token is exactly retrievable by attention. Quality at long context scales with cache — and so do cost, latency, and OOMs: each new token attends over all cached tokens, O(T²) without eviction, compression, or retrieval.

The pressure is cost per token at long context. Linear attention, state-space models, and fixed recurrent alternatives collapse the cache into a fixed-shape state updated incrementally: O(1) memory, O(T) compute. Technically small, consequentially large: per-token slots become an additive matrix with per-step updates — BDH-CQ's paper notes the special case where state accumulates additively per demonstration. The price is interference: non-orthogonal keys sharing directions overwrite each other, so exact recall degrades once n ≫ capacity.

Our artifact makes this tactile: a filing cabinet (KV `Map`, grows per pair) beside a whiteboard with 5 switchable write/read cartoons — hash (last wins), mamba-gate (salient kept), delta (blend to neither value), hola (+8 exact cache), bdh-ρ (decay fades old). At 120 pairs / 32 slots collisions already appear; flooding to 500→16 craters each rule differently while KV stays 100%. Clicking a yellow cell names the thieves — the gap is the lesson. All 5 labeled cartoons, not real kernels.

Three points on the frontier: (1) Mamba / selective SSMs (Gu & Dao, 2024): input-gated compact state, strong throughput, weak verbatim needle recall. (2) HOLA (Cui, arXiv:2607.02303, 2026): delta-rule compressive state plus a bounded exact cache for surprising pairs; 340M/15B tokens cuts Wiki perplexity 27.32→22.92 and holds RULER recall to 32K (16× train length). Its abstract states our claim independently: O(1) at the cost of lossy exact memory. (3) BDH / BDH-CQ (Pathway, arXiv:2509.26507, arXiv:2608.09888): Post-Transformer where memory is synaptic state via Hebbian writes (ρ_{t−1}=Σ v*xᵀU^{t−τ}, Eqs.4–5; Hebbian view 6–8), not token drawers. BDH-GPU uses ReLU low-rank maps + linear attention — explicitly not a Mamba SSM.

| Family | Memory | Recall | Bill | Signal |
|---|---|---|---|---|
| Transformer KV | O(n) | perfect | O(T²) | attention maps |
| Mamba SSM | O(1) gated | lossy far | cheap | selectivity |
| HOLA | O(1)+cache | recovered | cheap+cache | surprise β‖e‖ |
| BDH / CQ | O(1) synaptic | sags w/ load | lowest $/task shown | ~5% sparse, monosemantic synapses |

Evidence, correctly labeled: 134M BDH reaches 95% at 32K → 82% at 128K on BABILong QA1–QA5 (pathway.com homepage; vendor-reported, pending contamination/independent/leaderboard review) — the toy's sag at real scale. BDH-CQ reaches 29.5% pass@2 on ARC-AGI-1 at computed ~$0.0007/task, ~11× cheaper than GPT-5.6 Luna Low at 34.2% in Pathway's table — a Pareto cost-efficiency claim on one self-reported benchmark, checkpoint unreleased, not raw SOTA. Live toy curves reproduce the shape; vendor numbers are precomputed cards.

BDH is the O(1)-by-design case study; BDH-CQ is sibling proof the family trades accuracy for intelligence-per-dollar via latent recurrence without chain-of-thought. Where BDH has no role, we say so — here it is central.

Limitation that matters: forgetting is silent (no validity flag), and session adaptation (S_t updates) is not durable learning; fast-to-slow consolidation is open. Next: BDH App.E toy code, HOLA §2–3 parametric vs semiparametric readout, Pathway Equations of Reasoning blog.
