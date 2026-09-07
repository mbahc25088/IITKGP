# References — Cloud 9 (accessed 8 Sep 2026)

All links verified live. No paper PDFs redistributed; cite via arXiv + publisher pages.

1. Kosowski, Uznański, Chorowski, Stamirowska, Bartoszkiewicz. **The Dragon Hatchling: The Missing Link between the Transformer and Models of the Brain.** arXiv:2509.26507 [cs.NE], 30 Sep 2025. https://arxiv.org/abs/2509.26507
   - Supports: BDH architecture, BDH-GPU Eqs.4–5 (attention state ρ), Hebbian view Eqs.6–8, App.E toy code, ReLU low-rank + linear attention (not Mamba SSM). Used in artifact §3 BDH module + README §7.

2. Engdahl, Kosowski, Chorowski, Stamirowska, Uznański, Jiang, Phadke, Kinas, et al. **BDH-CQ: In-Context Learning with Recurrent Latent Reasoning.** arXiv:2608.09888 [cs.NE], 10 Aug 2026. https://arxiv.org/abs/2608.09888
   - Supports: S_t=U(S_{t−1},D_t), no eval-task demos in training, no weight updates at inference, 150M 29.5% pass@2 ARC-AGI-1 at computed ~$0.0007/task (Pareto claim). Used in BDH-CQ evidence card.

3. Cui, Wanyun. **A Hippocampus for Linear Attention: An Exact Memory for What the Recurrent State Forgets.** arXiv:2607.02303 [cs.AI], 2 Jul 2026. https://arxiv.org/abs/2607.02303
   - Supports: independent O(1)-but-lossy statement — fixed recurrent state overwritten under competing key–value writes; HOLA +8-cache design, Wiki 27.32→22.92, RULER to 32K. Used for claim + hola rule + comparison table.

4. Gu & Dao. **Mamba: Linear-Time Sequence Modeling with Selective State Spaces.** arXiv:2312.00752, 2024 (version as cited by BDH). https://arxiv.org/abs/2312.00752
   - Supports: selective SSM baseline; BDH cites as related work but architecturally distinct. Used in comparison table + BDH ≠ SSM disclaimer.

5. Pathway homepage (vendor page, not a paper). https://pathway.com/ — BABILong QA1–QA5 134M BDH 95%@32K → 82%@128K.
   - Supports: precomputed cost-of-exactness point. Labeled vendor-reported, pending contamination / independent / leaderboard review. Not an independent reproduction.
