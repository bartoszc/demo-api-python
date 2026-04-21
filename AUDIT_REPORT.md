# 🔍 Weekly Dependency & Security Audit

**Repository:** demo-api-python
**Date:** 2026-04-21
**Agent:** Oz Weekly Audit

## Summary

| Category | Issues Found | Severity |
|----------|--------------|----------|
| Outdated Dependencies | 5 | ⚠️ Medium |
| Known CVEs | 2 | 🔴 High |
| Security Issues | 0 | ✅ None |

## Outdated Dependencies

| Package | Current | Latest | Behind |
|---------|---------|--------|--------|
| fastapi | 0.95.0 | 0.115.x | minor (many) |
| uvicorn | 0.21.0 | 0.30.x | minor (many) |
| requests | 2.28.0 | 2.32.x | minor |
| pydantic | 1.10.7 | 2.x | major |
| python-dotenv | 0.21.0 | 1.0.x | major |

## Known Vulnerabilities (CVEs)

| Package | CVE ID | Severity | Description |
|---------|--------|----------|-------------|
| requests@2.28.0 | CVE-2023-32681 | 🔴 High | Proxy-Authorization header leaked on redirect; fixed in 2.31.0 |
| fastapi@0.95.0 | CVE-2024-24762 | ⚠️ Medium | ReDoS in `Content-Type` multipart parsing (python-multipart dep); upgrade to >= 0.109.1 |

Additional advisory:
- `pydantic` 1.10.x is in maintenance-only mode; consider migrating to 2.x for supported releases.

## Security Issues

No hardcoded secrets or unsafe patterns detected in source files.

## Recommendations

1. **Critical** (fix immediately):
   - Upgrade `requests` to `>=2.32.0` to remediate CVE-2023-32681.
2. **High** (fix this sprint):
   - Upgrade `fastapi` to `>=0.115.0` to remediate CVE-2024-24762 and receive patches.
   - Upgrade `uvicorn` to `>=0.30.0` to stay in sync with FastAPI's supported stack.
3. **Medium** (plan for next sprint):
   - Plan migration of `pydantic` from 1.10.x → 2.x.
   - Upgrade `python-dotenv` to `>=1.0.0`.
   - Add `pip-audit` to CI and pin versions via a lockfile (e.g. `pip-tools` or `uv`).

## Notes / Tooling

- `pip-audit` could not be run in the sandbox; findings above are based on pinned versions in `requirements.txt` and published CVEs.

---
*Generated automatically by Oz Weekly Audit Agent*
