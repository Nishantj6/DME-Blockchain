# Findings Board — Assurance Passports Paper
**Generated:** 2026-03-09
**Document:** main.tex + sections/*.tex + references.bib
**Pass 1 Agents:** paper-critic, domain-reviewer-blockchain, domain-reviewer-zk, domain-reviewer-dme, methodology-reviewer, proofreader

---

## Section: Evaluation (Section VII)

### [Critical] All evaluation data is TBD [source: paper-critic]
**Location:** evaluation.tex:44-163 (Tables 3-6, Figures 2-3)
**Description:** Every quantitative result in the Evaluation section is a TBD placeholder. Tables 3, 4, 5, and 6 contain no data. Figures 2 and 3 are empty placeholder boxes. The Discussion of Results (VII-F) draws conclusions from nonexistent data.
**Suggested fix:** Run experiments and fill all TBD values before submission.

### [Critical] Abstract and Conclusion claim completed benchmarks that don't exist [source: methodology-reviewer]
**Location:** main.tex:41, conclusion.tex:13-14
**Description:** Abstract says "with benchmarks across IBFT, QBFT, and Raft." Conclusion says "The evaluation demonstrates that ZK-based artifact attestation is feasible." These are false claims given TBD data.
**Suggested fix:** Rewrite abstract/conclusion after filling evaluation data, or qualify as "planned evaluation."

### [Critical] Discussion of Results presents predictions as findings [source: methodology-reviewer]
**Location:** evaluation.tex:169-182
**Description:** Four "key observations" are written in present tense as post-hoc analysis but reference no actual measurements.
**Suggested fix:** Rewrite as hypotheses until data exists.

### [Critical] All figures are placeholder fbox diagrams [source: paper-critic]
**Location:** framework.tex:97-103, architecture.tex:19-29, evaluation.tex:62-67, evaluation.tex:133-138
**Description:** Figures 1-4 are all \fbox text placeholders. IEEE Access requires actual figures.
**Suggested fix:** Create proper diagrams (lifecycle, architecture, scaling plot, throughput plot).

---

## Section: Bibliography

### [Critical] 7 bib entries have "Various" placeholder authors [source: paper-critic, proofreader]
**Location:** references.bib lines 108, 119, 131, 141, 177, 219, 284
**Description:** zkp_supply_chain2024, maritime_zkp2025, zkp_survey2025, zkp_frameworks_survey2025, dpp_did_vc2024, dme_framework2024, wells2023hotstuff_goquorum all have "Various" as author.
**Suggested fix:** Look up actual author lists via DOIs.

### [Major] Malformed author field in zkp_survey2025 [source: proofreader]
**Location:** references.bib:131
**Description:** `author={R, Various and others}` will render as "R. Various et al." — nonsensical.
**Suggested fix:** Fix immediately with actual authors.

### [Major] 4+ uncited bibliography entries [source: proofreader]
**Location:** references.bib
**Description:** zkp_survey2025, zkp_frameworks_survey2025, martin2023uaf_me, dme_framework2024 do not appear to be cited in any .tex file.
**Suggested fix:** Cite or remove.

### [Minor] Multiple bib entries use "and others" instead of full author lists [source: proofreader]
**Location:** references.bib (jagannath2025zksnark, kuhn2017digital_twin_blockchain, harz2020permissioned, yue2021/2023, dod_me_guide2023, martin2023uaf_me)
**Description:** Partial author lists. IEEE requires complete author information.
**Suggested fix:** Verify and complete all author lists.

---

## Section: Introduction

### [Minor] "Assurance Passport" capitalization inconsistent [source: proofreader]
**Location:** introduction.tex:21 (capitalized) vs abstract/rest of paper (lowercase)
**Description:** First proposal uses \emph{Assurance Passport} (capitalized) but abstract and all other running text uses lowercase.
**Suggested fix:** Lowercase to \emph{assurance passport} in introduction.tex:21.

### [Minor] "authorized provenance" should be "authorized origin" [source: proofreader]
**Location:** introduction.tex:22
**Description:** Inconsistent with the formal predicate name used everywhere else.
**Suggested fix:** Change to "authorized origin."

### [Minor] "ZK-SNARKs" inconsistent casing [source: proofreader]
**Location:** introduction.tex:37
**Description:** Uses "ZK-SNARKs" while rest of paper uses "zk-SNARKs."
**Suggested fix:** Change to "zk-SNARKs."

### [Minor] Missing "Nano" in "four NVIDIA Jetson boards" [source: proofreader]
**Location:** introduction.tex:32 (contribution 3)
**Description:** Every other reference says "Jetson Nano" but this one says just "Jetson boards."
**Suggested fix:** Change to "four NVIDIA Jetson Nano boards."

### [Minor] DDIL expanded twice in introduction body [source: proofreader]
**Location:** introduction.tex:9 and introduction.tex:26
**Description:** Redundant expansion. IEEE style: expand once in body text.
**Suggested fix:** Remove expansion at line 26, use "DDIL" alone.

---

## Section: Related Work (Section II)

### [Minor] No mention of broader ZKP landscape beyond Groth16 [source: paper-critic]
**Location:** related-work.tex
**Description:** PLONK and STARKs are mentioned only in Discussion trade-offs. No Related Work coverage of Marlin, Plonky2, Nova, Halo2.
**Suggested fix:** Add brief paragraph in Related Work or acknowledge scope limitation.

---

## Section: Preliminaries (Section III)

### [Minor] QBFT characterization as "reduces message complexity" is vague [source: domain-reviewer-blockchain]
**Location:** preliminaries.tex:72
**Description:** QBFT's primary improvement is better liveness guarantees and formal specification, not necessarily reduced message complexity.
**Suggested fix:** Soften to "QBFT refines IBFT with improved liveness guarantees and a formally verified specification."

### [Minor] Missing citation for BN254 security downgrade [source: domain-reviewer-zk]
**Location:** preliminaries.tex:49
**Description:** Claims "100-110 bits of security" but does not cite Kim-Barbulescu 2016 or Barbulescu-Duquesne 2019.
**Suggested fix:** Add citation for the NFS results.

---

## Section: Threat Model (Section IV)

### [Major] Proof predicates placed before framework definition [source: paper-critic]
**Location:** threat-model.tex (Section IV) vs framework.tex (Section V)
**Description:** Formal predicate equations (Eqs. 1-4) appear before the reader understands what an assurance passport is. Forces readers to take predicates on faith.
**Suggested fix:** Either move predicates to Framework section or defer formal equations, keeping only adversaries + security goals in threat model.

### [Minor] Update rules R not listed as public input for version validity [source: domain-reviewer-zk]
**Location:** threat-model.tex:62-66
**Description:** Eq. 4 shows public inputs as (c_i^v, c_i^{v+1}), but R is consortium-configurable. If hardcoded in circuit, state explicitly; if parameterized, must be public input.
**Suggested fix:** Clarify whether R is circuit-hardcoded or parameterized.

### [Minor] Transformation f_tau scope unclear [source: domain-reviewer-zk]
**Location:** threat-model.tex:75-80
**Description:** 60K constraint estimate may be optimistic for non-trivial transformations. Paper doesn't clarify what class of transformations is supported.
**Suggested fix:** State whether f_tau is restricted to simple operations or covers arbitrary transformations.

### [Minor] No adversary model for DME platform itself [source: methodology-reviewer]
**Location:** threat-model.tex (scope section)
**Description:** The adapter trusts Kompozition's API exports. A compromised or buggy DME platform that silently alters exports would undermine the commitment chain.
**Suggested fix:** Acknowledge as a trust assumption in Section IV scope.

---

## Section: Framework (Section V)

### [Major] Self-issuance justification repeated 3 times [source: paper-critic]
**Location:** framework.tex:69-78, framework.tex:202-204, discussion.tex:66-70
**Description:** Same argument appears in Phase 3, Security Analysis, and Discussion trade-offs.
**Suggested fix:** Consolidate — brief justification in Framework with forward-reference to Discussion.

### [Major] "Why not signed hashes?" argument appears 3 times [source: paper-critic]
**Location:** related-work.tex:94-97, threat-model.tex:48, evaluation.tex:143-163
**Description:** Same conceptual point made three times across different sections.
**Suggested fix:** Single authoritative treatment in Related Work, reference elsewhere.

---

## Section: Architecture (Section VI)

### [Minor] Private transactions: public vs private state unclear [source: domain-reviewer-blockchain]
**Location:** architecture.tex
**Description:** Paper mentions GoQuorum supports private transactions but never clarifies that registry contracts use public state.
**Suggested fix:** Add one sentence confirming public state usage; ZK proofs provide the privacy layer, not GoQuorum's Tessera.

### [Minor] Multi-sig governance implementation unspecified [source: domain-reviewer-blockchain]
**Location:** architecture.tex:108-109
**Description:** 3-of-4 multi-sig for key rotation mentioned but implementation approach not specified (governance contract, Gnosis Safe, native permissioning).
**Suggested fix:** One sentence clarifying approach.

### [Minor] Poseidon sponge: ~127-bit not 128-bit collision resistance [source: domain-reviewer-zk]
**Location:** architecture.tex:60
**Description:** Capacity c=1 on BN254 gives ~254 bits capacity, hence ~127-bit collision resistance. The "2× safety margin" claim is the operative statement.
**Suggested fix:** Adjust to "approximately 128-bit" or "~127-bit."

---

## Section: Discussion (Section VIII)

### [Minor] SysML v2 mentioned briefly but not developed [source: domain-reviewer-dme]
**Location:** discussion.tex:121
**Description:** SysML v2's formal JSON interchange format would simplify canonical serialization. Deserves more attention for 2026 submission.
**Suggested fix:** Add a sentence in Preliminaries about SysML v2 API standardization.

### [Minor] No INCOSE references [source: domain-reviewer-dme]
**Location:** N/A
**Description:** INCOSE is the primary professional body for SE. Missing references to INCOSE SE Vision 2035 or Digital Engineering Transformation.
**Suggested fix:** Cite INCOSE in introduction or related work.

### [Minor] Kompozition description is thin [source: domain-reviewer-dme]
**Location:** architecture.tex:123
**Description:** No citation, no metamodel description, no availability info for Kompozition.
**Suggested fix:** Add footnote or parenthetical describing vendor, metamodel, availability.

---

## Section: Conclusion (Section IX)

### [Critical] Conclusion overstates results [source: paper-critic]
**Location:** conclusion.tex:13-14
**Description:** Claims "deployed and evaluated" and "evaluation demonstrates feasibility" — these are false given TBD data.
**Suggested fix:** Rewrite after filling data.

---

## Cross-Cutting (not section-specific)

### [Major] No algorithm pseudocode anywhere [source: paper-critic]
**Location:** N/A
**Description:** Passport lifecycle (Commit, Prove, Issue, Verify) described only in prose. Systems papers benefit from at least one algorithm block.
**Suggested fix:** Add Algorithm 1 for passport issuance or verification workflow.

### [Major] Proof predicate descriptions stated 3 times [source: paper-critic]
**Location:** abstract, threat-model.tex (Sec IV-C), architecture.tex (Sec VI-B)
**Description:** What each predicate proves is described in overlapping prose across three locations.
**Suggested fix:** Architecture should reference threat model definitions without restating.

### [Major] "Tension between transparency and confidentiality" phrase used 5 times [source: paper-critic]
**Location:** abstract, introduction, related-work, discussion, conclusion
**Description:** Five occurrences of the same phrase is excessive.
**Suggested fix:** Use prominently once (Introduction), vary language elsewhere.

### [Major] Constraint counts are approximate and unvalidated [source: methodology-reviewer]
**Location:** architecture.tex (Table 2), evaluation.tex (Table 3)
**Description:** "~50K," "~80K" etc. should be exact values from circom --inspect output once circuits are compiled.
**Suggested fix:** Report exact constraint counts from compiled circuits.

### [Major] Missing load generation methodology for throughput tests [source: methodology-reviewer]
**Location:** evaluation.tex
**Description:** Number of client threads, arrival model, ramp-up period not specified. Essential for reproducibility.
**Suggested fix:** Specify load generation methodology when filling TBD data.

### [Minor] DDIL suitability stated in 5+ locations [source: paper-critic]
**Location:** abstract, introduction, architecture, evaluation, discussion
**Description:** Repetitive without adding new information each time.
**Suggested fix:** Reduce to authoritative treatment in architecture + discussion.

### [Minor] SRR and PDR not expanded at first use [source: domain-reviewer-dme]
**Location:** framework.tex:165
**Description:** "System Requirements Review" and "Preliminary Design Review" used as examples but not expanded for IEEE Access audience.
**Suggested fix:** Expand at first use.

### [Minor] Batched ecPairing optimization not mentioned [source: domain-reviewer-blockchain, domain-reviewer-zk]
**Location:** evaluation.tex:91-96, framework.tex:151
**Description:** Batching 16 pairs into single ecPairing call saves ~102,000 gas (~12%). Current approach uses 4 separate calls.
**Suggested fix:** Mention optimization opportunity and trade-off (batching prevents selective verification).

### [Minor] Missing formal security reduction for at least one goal [source: methodology-reviewer]
**Location:** framework.tex:186-208
**Description:** Journal venue (IEEE Access) may expect at least one game-based reduction, preferably for Goal 5 (predicate attestation).
**Suggested fix:** Add one formal reduction or justify deferral more strongly.

### [Minor] Missing proving key sizes and circuit compilation times [source: methodology-reviewer]
**Location:** evaluation.tex
**Description:** One-time costs but relevant for deployment planning on 4GB devices.
**Suggested fix:** Add to evaluation when running experiments.

### [Minor] IBFT version ambiguous [source: domain-reviewer-blockchain]
**Location:** preliminaries.tex:67
**Description:** GoQuorum supported legacy IBFT and IBFT 2.0. Paper doesn't specify which.
**Suggested fix:** Clarify "legacy IBFT" or "IBFT 1.0."

### [Minor] BN254 security level not surfaced as defense limitation [source: methodology-reviewer]
**Location:** preliminaries.tex:49
**Description:** 100-110 bits may be insufficient for defense applications. Migration to BLS12-381 mentioned but only in preliminaries.
**Suggested fix:** Surface in Discussion limitations section.

### [Minor] ASOT federated model not acknowledged [source: domain-reviewer-dme]
**Location:** preliminaries.tex:108-118
**Description:** Paper treats ASOT as single repository. Many DME programs use federated ASOT. Architecture naturally supports federation.
**Suggested fix:** Add sentence acknowledging federated ASOT models.

### [Minor] Unused label sec:fw-revocation [source: proofreader]
**Location:** framework.tex:126
**Description:** Label defined but never referenced.
**Suggested fix:** Remove or use.
