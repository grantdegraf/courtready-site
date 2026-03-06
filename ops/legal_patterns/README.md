# Legal Patterns

Persistent memory of legal issue patterns across all analyzed cases.

## Record Format

File naming: `pattern_<case_id>.json`

## Fields

- `case_name`
- `court_department`
- `legal_issue_type`
- `issue_signals`
- `precedent_conflicts`
- `conflict_score`
- `decision_date`

## Pattern Alerts

Stored in `ops/legal_patterns/pattern_alerts/`

Pattern alerts are **logged only** — they do not automatically trigger outreach.

## Pattern Detection Signals

- Multiple cases involving same legal issue
- Department-specific doctrinal inconsistency
- Statutory analysis omissions
