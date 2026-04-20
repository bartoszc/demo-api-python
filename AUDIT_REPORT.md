# 🔍 Weekly Dependency & Security Audit

**Repository:** demo-api-python
**Date:** 2026-04-20
**Agent:** Oz Weekly Audit

## Summary

| Category | Issues Found | Severity |
|----------|--------------|----------|
| Outdated Dependencies | 5 | ⚠️ Medium |
| Known CVEs | 15 (across 5 packages incl. transitive) | 🔴 High |
| Security Issues | 0 | ✅ None |

Tooling used: `pip-audit 2.10.0`, `pip index versions`.

## Outdated Dependencies

| Package | Current | Latest | Behind |
|---------|---------|--------|--------|
| fastapi       | 0.95.0   | 0.136.0 | minor (many releases) |
| uvicorn       | 0.21.0   | 0.44.0  | minor (many releases) |
| requests      | 2.28.0   | 2.33.1  | minor                 |
| pydantic      | 1.10.7   | 2.13.3  | major                 |
| python-dotenv | 0.21.0   | 1.2.2   | major                 |

## Known Vulnerabilities (CVEs)

### Direct dependencies

| Package | CVE / ID | Fixed in | Description |
|---------|----------|----------|-------------|
| fastapi==0.95.0   | [PYSEC-2024-38](https://osv.dev/vulnerability/PYSEC-2024-38) | 0.109.1 | ReDoS when parsing form data with `Content-Type: multipart/form-data` |
| pydantic==1.10.7  | [CVE-2024-3772](https://nvd.nist.gov/vuln/detail/CVE-2024-3772) | 1.10.13 / 2.4.0 | ReDoS in email validation regex |
| requests==2.28.0  | [PYSEC-2023-74](https://osv.dev/vulnerability/PYSEC-2023-74) | 2.31.0 | Leaks `Proxy-Authorization` headers on redirect |
| requests==2.28.0  | [CVE-2024-35195](https://nvd.nist.gov/vuln/detail/CVE-2024-35195) | 2.32.0 | TLS verification bypass across Session requests when first used with `verify=False` |
| requests==2.28.0  | [CVE-2024-47081](https://nvd.nist.gov/vuln/detail/CVE-2024-47081) | 2.32.4 | `.netrc` credential leak via URL parsing issue |
| requests==2.28.0  | [CVE-2026-25645](https://nvd.nist.gov/vuln/detail/CVE-2026-25645) | 2.33.0 | Predictable filenames in `extract_zipped_paths()` |

### Transitive dependencies

| Package | CVE / ID | Fixed in | Description |
|---------|----------|----------|-------------|
| starlette==0.26.1 | [PYSEC-2023-83](https://osv.dev/vulnerability/PYSEC-2023-83) | 0.27.0 | Directory traversal in `StaticFiles` |
| starlette==0.26.1 | [CVE-2024-47874](https://nvd.nist.gov/vuln/detail/CVE-2024-47874) | 0.40.0 | DoS via multipart form parts without filename buffered in memory |
| starlette==0.26.1 | [CVE-2025-54121](https://nvd.nist.gov/vuln/detail/CVE-2025-54121) | 0.47.2 | Large multipart uploads block event loop |
| urllib3==1.26.20  | [CVE-2025-50181](https://nvd.nist.gov/vuln/detail/CVE-2025-50181) | 2.5.0   | Retry/redirect logic control issue |
| urllib3==1.26.20  | [CVE-2025-66418](https://nvd.nist.gov/vuln/detail/CVE-2025-66418) | 2.6.0   | Chained content-encoding handling issue |
| urllib3==1.26.20  | [CVE-2025-66471](https://nvd.nist.gov/vuln/detail/CVE-2025-66471) | 2.6.0   | Streaming API vulnerability |
| urllib3==1.26.20  | [CVE-2026-21441](https://nvd.nist.gov/vuln/detail/CVE-2026-21441) | 2.6.3   | Streaming API vulnerability |

## Security Issues

No hardcoded secrets or risky patterns detected in `app.py`.

## Recommendations

1. **Critical (fix immediately):**
   - Upgrade `requests` to `>=2.33.0` (4 CVEs, including credential/header leaks & TLS bypass).
   - Upgrade `fastapi` to `>=0.109.1` (fixes ReDoS; latest `0.136.0` recommended). This also pulls a patched `starlette`.
   - Upgrade `pydantic` to `>=1.10.13` (or migrate to 2.x for long-term support).
2. **High (this sprint):**
   - Plan the `pydantic` v1 → v2 migration; v1 is in maintenance-only mode.
   - Upgrade `uvicorn` to `>=0.44.0`.
3. **Medium (next sprint):**
   - Upgrade `python-dotenv` to `>=1.2.2`.
   - Pin direct deps with `~=` or a lockfile (e.g. `pip-tools` / `uv`) to stabilize transitive graph.
   - Add `pip-audit` to CI pipeline.

### Suggested updated `requirements.txt`

```
fastapi==0.136.0
uvicorn==0.44.0
requests==2.33.1
pydantic==2.13.3
python-dotenv==1.2.2
```

***
*Generated automatically by Oz Weekly Audit Agent*
