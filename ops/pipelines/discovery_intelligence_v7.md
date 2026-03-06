# CourtReady Discovery Intelligence — v7.0

## Updated Pipeline

```
case_discovery
  → legal_issue_detection       [NEW — v7.0]
  → precedent_conflict_detection [NEW — v7.0]
  → case_pattern_memory          [NEW — v7.0]
  → opportunity_scoring          [UPDATED — v7.0]
  → batch_queue
```

---

## Module 1: Legal Issue Detection

For every discovered decision:

1. Retrieve full opinion text
2. Scan for high-probability appellate issue phrases:
   - `"self-serving affidavit"`
   - `"no triable issue of fact"`
   - `"failed to raise a triable issue"`
   - `"unsupported by evidence"`
   - `"not in admissible form"`
   - `"inadmissible hearsay"`
   - `"lack of foundation"`
3. Classify into flag categories:
   - `summary_judgment_evidence_handling`
   - `evidentiary_standard_application`
   - `coverage_analysis_gap`
   - `incomplete_statutory_analysis`
4. Generate `issue_signals` array
5. Store in `ops/case_analysis/case_<case_id>_analysis.json`

---

## Module 2: Precedent Conflict Detection

After issue signals are generated:

1. Search for controlling precedent on detected issue
   - Sources: Court of Appeals decisions, prior AD rulings, statutory interpretations
2. Compare decision rule vs. precedent rule
3. If conflict detected:
   - Set `precedent_conflict_detected = true`
   - Add `precedent_conflicts` (e.g., `["Zuckerman v City of New York", "Alvarez v Prospect Hospital"]`)
   - Assign `precedent_conflict_score`
4. Elevated opportunity score for precedent conflicts

---

## Module 3: Case Pattern Memory

1. Store structured issue record for every analyzed case in `ops/legal_patterns/pattern_<case_id>.json`
2. Analyze stored records for recurring patterns
3. Generate pattern alerts when patterns detected
4. Store alerts in `ops/legal_patterns/pattern_alerts/`
5. Pattern alerts are **logged only** — no automatic outreach

---

## Updated Opportunity Scoring Formula

| Factor | Weight |
|--------|--------|
| `issue_strength` | 40% |
| `precedent_conflict_score` | 30% |
| `decision_recency` | 20% |
| `practice_area_relevance` | 10% |

**Score range: 0–100. Cases scoring ≥ 60 proceed to batch review.**

---

## System Rules

1. Discovery must prioritize **legal reasoning signals** over case metadata alone
2. Cases with precedent conflicts receive **elevated opportunity scores**
3. Pattern alerts logged but do **not** automatically trigger outreach
