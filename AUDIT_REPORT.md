# 🔍 Weekly Dependency & Security Audit

**Repository:** demo-api-python
**Date:** 2026-04-21
**Agent:** Oz Weekly Audit

## Summary

| Category | Issues Found | Severity |
|----------|--------------|----------|
| Outdated Dependencies | 5 | ⚠️ Medium |
| Known CVEs (pip-audit) | 16 across 6 packages | 🔴 High |
| Security Issues (hardcoded secrets) | 0 | ✅ None |

## Outdated Dependencies

| Package | Current | Latest | Behind |
|---------|---------|--------|--------|
| fastapi | 0.95.0 | 0.136.0 | many minor releases |
| uvicorn | 0.21.0 | 0.45.0 | many minor releases |
| requests | 2.28.0 | 2.33.1 | minor |
| pydantic | 1.10.7 | 2.13.3 | major (v1 → v2) |
| python-dotenv | 0.21.0 | 1.2.2 | major |

## Known Vulnerabilities (CVEs)

| Package | Version | CVE / PYSEC | Advisory | Fix Version |
|---------|---------|-------------|----------|-------------|
| fastapi | 0.95.0 | CVE-2024-24762 (PYSEC-2024-38) | ReDoS in `python-multipart` Content-Type parsing | 0.109.1 |
| pydantic | 1.10.7 | CVE-2024-3772 (GHSA-mr82-8j83-vxmv) | ReDoS via crafted email string | 1.10.13 / 2.4.0 |
| requests | 2.28.0 | CVE-2023-32681 (PYSEC-2023-74) | `Proxy-Authorization` header leak on redirect | 2.31.0 |
| requests | 2.28.0 | CVE-2024-35195 (GHSA-9wx4-h78v-vm56) | `verify=False` persists on pooled session connection | 2.32.0 |
| requests | 2.28.0 | CVE-2024-47081 (GHSA-9hjg-9r4m-mvj7) | `.netrc` credential leak on crafted URLs | 2.32.4 |
| requests | 2.28.0 | CVE-2026-25645 (GHSA-gc5v-m9x4-r6x2) | `extract_zipped_paths` predictable temp path | 2.33.0 |
| python-dotenv | 0.21.0 | CVE-2026-28684 (GHSA-mf9w-mj56-hr94) | `set_key`/`unset_key` follow symlinks → arbitrary file overwrite | 1.2.2 |
| starlette (transitive via fastapi) | 0.26.1 | CVE-2023-29159 (PYSEC-2023-83) | Path traversal in `StaticFiles` | 0.27.0 |
| starlette | 0.26.1 | CVE-2024-47874 (GHSA-f96h-pmfr-66vw) | DoS: unbounded form-field buffering | 0.40.0 |
| starlette | 0.26.1 | CVE-2025-54121 (GHSA-2c2j-9gv5-cj73) | Event-loop blocking on multipart rollover | 0.47.2 |
| urllib3 (transitive via requests) | 1.26.20 | CVE-2025-50181 (GHSA-pq67-6m6q-mj2v) | `PoolManager(retries=...)` redirect-disable ignored | 2.5.0 |
| urllib3 | 1.26.20 | CVE-2025-66418 (GHSA-gm62-xv2j-4w53) | Unbounded chained decompression → DoS | 2.6.0 |
| urllib3 | 1.26.20 | CVE-2025-66471 (GHSA-2xpw-w6gg-jr37) | Streaming API over-decompresses untrusted content | 2.6.0 |
| urllib3 | 1.26.20 | CVE-2026-21441 (GHSA-38jv-5279-wg99) | Redirect response decompressed even with `preload_content=False` | 2.6.3 |

## Security Issues

| File | Line | Issue | Recommendation |
|------|------|-------|----------------|
| _none_ | — | No hardcoded secrets/tokens detected in tracked source | — |

Note: `requirements.txt` pins only top-level deps; transitive pins are not tracked. A lockfile (`pip-compile`, `poetry.lock`, or `uv.lock`) would make transitive advisories actionable and reproducible.

## Recommendations

1. **Critical / High (fix immediately)**
   - Upgrade `requests>=2.33.0` (closes 4 CVEs, incl. proxy-auth leak and `verify=False` persistence).
   - Upgrade `python-dotenv>=1.2.2` (closes CVE-2026-28684 symlink-follow arbitrary file write).
   - Upgrade `fastapi>=0.109.1` (pulls fixed `starlette` / `python-multipart`, closes ReDoS).
   - Pin/upgrade `starlette>=0.47.2` if kept explicit.
2. **Medium (this sprint)**
   - Upgrade `pydantic` to `2.x` (plan migration – breaking changes in v2) or at minimum `1.10.13`.
   - Upgrade `urllib3>=2.6.3` (pulls in via modern `requests`).
   - Upgrade `uvicorn>=0.45.0`.
3. **Low (plan for next sprint)**
   - Introduce a lockfile (`pip-compile` / `poetry` / `uv`) and wire `pip-audit` into CI.
   - Enable Dependabot or Renovate on this repo.

***
*Generated automatically by Oz Weekly Audit Agent*
