# 🔍 Weekly Dependency & Security Audit

**Repository:** demo-api-python
**Date:** 2026-04-19
**Agent:** Oz Weekly Audit

## Summary

| Category | Issues Found | Severity |
|----------|--------------|----------|
| Outdated Dependencies | 5 | ⚠️ Medium |
| Known CVEs | 15 | 🔴 High |
| Security Issues | 0 | ✅ None |

Tools used: `pip-audit`, `pip index versions`.

## Outdated Dependencies

Direct dependencies from `requirements.txt`:

| Package | Current | Latest | Behind |
|---------|---------|--------|--------|
| fastapi | 0.95.0 | 0.136.0 | minor (many) |
| uvicorn | 0.21.0 | 0.44.0 | minor (many) |
| requests | 2.28.0 | 2.33.1 | minor |
| pydantic | 1.10.7 | 2.13.2 | **major** |
| python-dotenv | 0.21.0 | 1.2.2 | **major** |

## Known Vulnerabilities (CVEs)

`pip-audit` detected 15 vulnerabilities across 5 packages (direct + transitive):

| Package | Version | Advisory | Fix Version |
|---------|---------|----------|-------------|
| fastapi | 0.95.0 | PYSEC-2024-38 (ReDoS in python-multipart Content-Type parsing) | 0.109.1 |
| pydantic | 1.10.7 | CVE-2024-3772 (ReDoS via crafted email) | 1.10.13 / 2.4.0 |
| requests | 2.28.0 | PYSEC-2023-74 (Proxy-Authorization header leak on redirect) | 2.31.0 |
| requests | 2.28.0 | CVE-2024-35195 (session `verify=False` persistence) | 2.32.0 |
| requests | 2.28.0 | CVE-2024-47081 (`.netrc` credential leak via crafted URL) | 2.32.4 |
| requests | 2.28.0 | CVE-2026-25645 | 2.33.0 |
| starlette (transitive) | 0.26.1 | PYSEC-2023-83 (multipart DoS) | 0.27.0 |
| starlette (transitive) | 0.26.1 | CVE-2024-47874 (multipart DoS, large forms) | 0.40.0 |
| starlette (transitive) | 0.26.1 | CVE-2025-54121 | 0.47.2 |
| urllib3 (transitive) | 1.26.20 | CVE-2025-50181 | 2.5.0 |
| urllib3 (transitive) | 1.26.20 | CVE-2025-66418 | 2.6.0 |
| urllib3 (transitive) | 1.26.20 | CVE-2025-66471 | 2.6.0 |
| urllib3 (transitive) | 1.26.20 | CVE-2026-21441 | 2.6.3 |

## Security Issues

No hardcoded secrets detected in `app.py` or `requirements.txt`.

## Recommendations

1. **Critical** (fix immediately):
   - Upgrade `requests` to `>=2.32.4` to eliminate 4 CVEs including credential-leak issues.
   - Upgrade `fastapi` to `>=0.109.1` to eliminate the multipart ReDoS vector.
2. **High** (fix this sprint):
   - Upgrade `pydantic` to `>=2.4.0` (note: v2 API migration required).
   - Ensure `urllib3 >=2.6.3` and `starlette >=0.47.2` are pulled in transitively after the above upgrades.
3. **Medium** (plan for next sprint):
   - Upgrade `uvicorn` to `>=0.44.0` and `python-dotenv` to `>=1.2.2`.
   - Pin transitive deps explicitly (or add a lock file such as `pip-compile`/`uv lock`) to make future audits deterministic.

***
*Generated automatically by Oz Weekly Audit Agent*
