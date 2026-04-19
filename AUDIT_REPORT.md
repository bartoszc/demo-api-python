# 🔍 Weekly Dependency & Security Audit

**Repository:** bartoszc/demo-api-python
**Date:** 2026-04-19
**Agent:** Oz Weekly Audit

## Summary

| Category | Issues Found | Severity |
|----------|--------------|----------|
| Outdated Dependencies | 0 | ✅ None |
| Known CVEs | 0 | ✅ None |
| Security Issues | 1 | ⚠️ Low |

## Repository State

This repository currently contains **empty** tracked files:

- `app.py` — 0 bytes
- `requirements.txt` — 0 bytes
- `README.md` — 0 bytes

The latest commit (`2dacfff`) is titled _"init: FastAPI service with outdated deps"_ but no content has been
pushed yet, so there is nothing to audit at the dependency level.

## Outdated Dependencies

None — `requirements.txt` is empty.

## Known Vulnerabilities (CVEs)

None detected — no dependencies are declared.

## Security Issues

| File | Line | Issue | Recommendation |
|------|------|-------|----------------|
| `requirements.txt` | — | File is empty; no pinned dependency surface yet | Commit the intended FastAPI dependencies and re-run the audit |
| `app.py` | — | No application code to review | Commit application source once written |

Notes for future audits once code lands:

- Run `pip-audit -r requirements.txt` to cross-check against the Python advisory database.
- Run `pip list --outdated --format=json` (in a virtualenv with the requirements installed) to flag drift.
- Ensure FastAPI is pinned to a currently supported minor version (>=0.110) and that Starlette / Pydantic
  are not left floating to avoid indirect CVE exposure.

## Recommendations

1. **Critical (fix immediately):** _none_
2. **High (fix this sprint):** Commit the intended application code and pinned dependencies so the repository
   is actually auditable.
3. **Medium (plan for next sprint):** Add a `pip-audit` step to CI once `requirements.txt` is populated.

***
_Generated automatically by Oz Weekly Audit Agent_
