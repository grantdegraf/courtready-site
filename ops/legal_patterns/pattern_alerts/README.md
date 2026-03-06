# Pattern Alerts

Generated when recurring legal issue patterns are detected across multiple cases.

## Alert Format

File naming: `alert_<timestamp>.json`

## Fields

- `pattern_alert` — description of detected pattern
- `affected_cases` — count
- `case_ids` — list of case IDs involved
- `department` — court department (e.g., AD2)
- `legal_issue_type`
- `detected_at`

## Example

```json
{
  "pattern_alert": "late notice prejudice analysis inconsistency",
  "affected_cases": 4,
  "case_ids": ["case_001", "case_002", "case_003", "case_004"],
  "department": "AD2",
  "legal_issue_type": "coverage_analysis_gap",
  "detected_at": "2026-03-06T09:00:00Z"
}
```

## System Rule

Pattern alerts are **logged only** — they do NOT automatically trigger outreach.
