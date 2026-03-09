# Paper Review Report — 2026-03-09
## Assurance Passports: Privacy-Preserving Trust for DME via Consortium Blockchain and ZK Proofs

**Venue:** IEEE Access | **Stage:** Pre-submission draft | **Review mode:** Full (6 agents, 2 passes)

---

## Quality Score Card

| Dimension | Weight | Score | Notes |
|-----------|--------|-------|-------|
| Structure | /25 | 20/25 | Strong org, but predicate repetition (-3), redundant arguments (-2) |
| Technical Correctness | /25 | 22/25 | Sound ZK/blockchain/DME foundations, minor gaps (-3) |
| Novelty & Positioning | /25 | 23/25 | Clear gaps, strong comparison table, good two-axis positioning |
| Presentation & Writing | /25 | 17/25 | Good prose but ALL eval data TBD (-5), placeholder figures (-3) |
| Integration (seam) | bonus | +3 | Good cross-domain coherence |

**Framework Score: 85/100**
**Effective Score (with TBD penalty): ~60/100** -- below 80 commit threshold

The framework/theory sections are strong (~85), but the paper is **unpublishable** without evaluation data, proper figures, and the bibliography fixes applied in this review.

---

## Review Pipeline

- **Pass 1:** 6 agents (paper-critic, domain-reviewer-blockchain, domain-reviewer-zk, domain-reviewer-dme, methodology-reviewer, proofreader)
- **Pass 2:** 3 domain reviewers cross-informed with findings board
- **Seam verification:** Skipped (no three-way seam issues flagged)
- **Contradictions resolved:** 4 (ecPairing savings, tension phrase count, predicate placement, DoDAF)
- **Triage:** 5 DESIGN-CHOICE, 8 AUTO-FIX, 1 ESCALATE

---

## Revisions Applied (this session)

### Bibliography (Critical)
- Fixed 4 "Various" placeholder authors with actual author names:
  - `zkp_supply_chain2024`: Prasad, Tiwari, Chawla, Tomar
  - `maritime_zkp2025`: Silveirinha, Bhandari, Ferreira, Martins
  - `wells2023hotstuff_goquorum`: Wells, Lim, Festin, Tan
  - `dpp_did_vc2024`: Illan Garcia, Munoz-Escoi, Arjona Aroca, Fernandez-Bravo Penuela
- Removed 4 uncited entries: `zkp_survey2025`, `zkp_frameworks_survey2025`, `martin2023uaf_me`, `dme_framework2024`

### Proofreading Fixes
- introduction.tex: "Assurance Passport" -> "assurance passport" (lowercase consistency)
- introduction.tex: "authorized provenance" -> "authorized origin" (predicate name consistency)
- introduction.tex: Removed redundant DDIL expansion (was expanded twice in body)
- introduction.tex: "four NVIDIA Jetson boards" -> "four NVIDIA Jetson Nano boards"
- preliminaries.tex: QBFT "reduces message complexity" -> "improved liveness guarantees and formally verified specification"
- preliminaries.tex: Expanded "UAF" to "Unified Architecture Framework (UAF)"

### Technical Clarifications
- threat-model.tex: Added trust assumption (6) for DME platform API fidelity
- threat-model.tex: Clarified update rules R are circuit-hardcoded (different rule sets = separate circuits)
- architecture.tex: Added sentence confirming all registry contracts use public state (no Tessera)
- architecture.tex: Softened "128-bit" to "approximately 128-bit" collision resistance for Poseidon
- evaluation.tex: Added batched ecPairing optimization note (754K vs 856K gas)
- discussion.tex: Added "Concrete security level" limitation paragraph (BN254 100-110 bits, recommend BLS12-381)
- preliminaries.tex: Added federated ASOT model acknowledgment

---

## Action Plan (remaining items for user)

### MUST-FIX (blocking submission)

1. **Fill ALL TBD evaluation data** -- Tables 3-6 and Figures 2-3. Run experiments on Jetson Nano testbed. This is the single largest gap. Without data, the paper cannot be submitted.

2. **Create proper figures** -- Replace all \fbox placeholders:
   - Fig 1: Assurance passport lifecycle sequence diagram
   - Fig 2: 4-layer system architecture diagram
   - Fig 3: Proof generation time vs artifact size plot
   - Fig 4: Throughput vs concurrent load plot

3. **Rewrite abstract/conclusion** after filling evaluation data. Current text claims completed benchmarks that don't exist.

4. **Report exact constraint counts** from `circom --inspect` output, replacing "~50K", "~80K" etc.

5. **Specify load generation methodology** for throughput tests: client count, arrival model, measurement window.

6. **Specify GoQuorum block period and block gas limit** in experimental setup section.

7. **Report peak memory** for GoQuorum validator and SnarkJS prover separately (4GB Jetson constraint).

### SHOULD-FIX (improve acceptance chance)

8. **Add Algorithm 1** -- Pseudocode for passport verification or issuance workflow.

9. **Reduce repetition:**
   - Self-issuance justification: consolidate to Framework + brief Discussion reference
   - "Why not signed hashes?": single authoritative treatment in Related Work
   - "Tension between transparency and confidentiality": max 2 occurrences
   - Proof predicate descriptions: Architecture should reference Threat Model, not restate

10. **Add comparison with non-ZK privacy approaches** (TEEs, HE) -- even a qualitative paragraph in Discussion.

11. **Characterize synthetic test artifacts** -- state nesting depth, element count, relationship count, and how they compare to real SysML packages.

12. **Add Kompozition footnote** -- vendor, metamodel, commercial availability.

13. **Scope derivation lineage transformation f_tau** -- state which DME transformations qualify (deterministic model-to-model) vs which don't (human refinement).

14. **Fix remaining "and others" in bib entries** -- jagannath2025zksnark, kuhn2017digital_twin_blockchain, harz2020permissioned, yue2021/2023, dod_me_guide2023. Look up full author lists.

### NICE-TO-HAVE (polish)

15. Add BN254 NFS citation (Kim-Barbulescu 2016 or Barbulescu-Duquesne 2019).
16. Add PLONK citation in Discussion trade-offs.
17. Clarify IBFT version (legacy vs 2.0).
18. Add data availability statement per IEEE Access requirements.
19. Expand SRR/PDR at first use in framework.tex.
20. Remove unused \label{sec:fw-revocation}.
21. Mention SysML v2 JSON interchange format in Discussion or Preliminaries.
22. Note resource contention as liveness risk (not just operational concern) in threat model scope.

### DESIGN-CHOICE (user decision needed)

- **ecPairing batching:** Added optimization note. No further action needed unless user wants to implement batched verification.
- **Baseline credential authority privacy:** Authority identity is disclosed via conventional signature. ZK variant could hide it if needed. User decides if this warrants a sentence.
- **Proof predicate placement:** Current placement (threat model) is defensible. User can move to framework if preferred.
- **Configuration baseline milestone taxonomy:** Could map `d` to DoD milestone taxonomy (SRR, PDR, CDR, TRR). Optional enrichment.

### ESCALATE (needs user input)

- **Resource contention as liveness threat:** On 4GB Jetson, concurrent proof generation + GoQuorum validation could halt the network (n=4, f=1). The discussion acknowledges this but treats it as operational. Should this be elevated to threat model scope or is the current placement sufficient?

---

## Seam Analysis Summary

No three-way seam issues detected. Cross-domain coherence is good:
- ZK-Blockchain seam: Gas costs, proof bundling, commitment binding all consistent
- ZK-DME seam: Schema compliance scoping is honest; artifact size limitation acknowledged
- Blockchain-DME seam: DDIL liveness analysis is realistic; federated ASOT now acknowledged

Minor seam: Kompozition trust assumption was missing from threat model -- now fixed.

---

## Learnings (to append to learnings.md)

### Review Contradictions
- ecPairing batching savings: ZK reviewer estimated 12%, blockchain reviewer corrected to ~3.5% net after ecMul overhead. Both agree it's minor on zero-gas GoQuorum. [CONFIRMED]
- Proof predicate section placement: paper-critic recommended moving to framework; ZK reviewer defended current threat model placement. Both valid. [TENTATIVE - user choice]

### Seam Decisions
- Baseline credential uses conventional signature (not ZK) for configuration authority -- appropriate since commitment set is public on-chain. [CONFIRMED]
- Registry contracts use public state (no Tessera private transactions) -- ZK proofs provide the privacy layer. [CONFIRMED]
