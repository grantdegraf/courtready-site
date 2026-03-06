# Case Analysis

Outputs from the Legal Issue Detection module (v7.0).

## Record Format

File naming: `case_<case_id>_analysis.json`

## Fields

- `case_name`
- `case_id`
- `issue_signals` — detected phrase-level appellate issue indicators
- `flag_categories` — classified issue types
- `precedent_conflict_detected` — boolean
- `precedent_conflict_score` — 0–100
- `precedent_conflicts` — list of conflicting case citations
- `opportunity_score` — 0–100 (≥60 routes to batch queue)
- `analyzed_at`
