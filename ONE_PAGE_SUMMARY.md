# One-page concept summary — KV-Cache vs Fixed Recurrent State (Cloud 9, ~720 words)

Transformers remember by keeping everything. For each generated token the model stores its key and value vectors in a KV-cache, so memory grows linearly with length O(n) and any past token can be retrieved exactly by dot-product attention. This exactness is why long-context quality scales with cache size, and why inference cost, latency, and OOMs scale too: every new token pays attention over all cached tokens, O(T²) compute without compression, eviction, or retrieval tricks.

The design pressure is therefore cost per token at long context. Linear attention, state-space models, and fixed-size recurrent alternatives collapse the unbounded cache into a fixed-shape state updated incrementally (O(1) memory, O(T) compute). The change is technical and small to state: replace per-token slots with an additive matrix updated per demonstration or token. BDH-CQ's paper makes this explicit as contextual memory with the special case where state accumulates additively per demonstration. The trade-off is information-theoretic: non-orthogonal keys sharing state directions interfere, so earlier associations are overwritten and exact recall degrades once n ≫ state capacity.

Three representative efforts show different points on this frontier. (1) Mamba / selective SSMs (Gu & Dao, 2024): input-dependent gating over a compact state; strong long-sequence throughput, weaker verbatim needle recall than full attention. (2) HOLA — Hippocampal Linear Attention (Cui, arXiv:2607.02303, 2026): keeps a delta-rule compressive state plus a bounded exact KV cache for surprising pairs; at 340M/15B tokens cuts Wiki perplexity 27.32→22.92 and holds RULER needle recall to 32K (16× train length). Its abstract is nearly our claim verbatim: O(1) at the cost of lossy exact memory. (3) BDH / BDH-CQ (Pathway, arXiv:2509.26507, arXiv:2608.09888): brain-inspired Post-Transformer where memory is synaptic state updated by Hebbian writes as the model reads (attention state ρ_{t−1}=Σ v*xᵀU^{t−τ}, Eqs.4–5; Hebbian view Eqs.6–8), not token-indexed slots. BDH-GPU reformulates this with ReLU low-rank transforms + linear attention — explicitly not a Mamba-style SSM.

| System | Memory | Exact recall | Cost | Interpretability |
|---|---|---|---|---|
| Transformer KV | O(n) grows | perfect | high, O(T²) | attention maps |
| Mamba SSM | O(1) gated | lossy distant | low | selective dynamics |
| HOLA | O(1)+bounded cache | recovered via cache | low+cache | surprise signal β‖e‖ |
| BDH / BDH-CQ | O(1) synaptic ρ,S_t | lossy, degrades under load | lowest $/task shown | sparse (~5%), monosemantic synapses, scale-free |

Evidence with correct labels: vendor-reported BABILong QA1–QA5 with 134M BDH hits 95% at 32K, 82% at 128K (pathway.com; pending contamination/independent/leaderboard review) — same interference-under-load shape as the toy. Vendor-reported BDH-CQ hits 29.5% pass@2 on ARC-AGI-1 at computed $0.0007/task (11× cheaper than GPT-5.6 Luna Low at 34.2% in Pathway's comparison) — a cost-accuracy Pareto claim, not a raw-accuracy SOTA; single benchmark, self-reported, checkpoint unreleased. Our artifact reproduces the shape live (hash-modulo toy, n=10–500, N=16–256) and labels vendor numbers as precomputed.

BDH's role is direct: it is the O(1)-by-design case study. BDH-CQ's role is sibling evidence that the same family trades accuracy for intelligence-per-dollar via latent recurrence without chain-of-thought. If BDH has no role in a sub-claim, we say so; here it is central.

Key limitation: forgetting is silent — no validity flag — and within-session adaptation (S_t updates) is not durable cross-session learning; fast-to-slow consolidation stays open. Next: read the BDH paper App.E toy code, then HOLA §2–3 for the parametric vs semiparametric readout, then Pathway's Equations of Reasoning blog.
