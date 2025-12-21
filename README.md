# Security Summary Action

Generate a comprehensive summary of security scan results for GitHub Actions workflows, including CodeQL Analysis, Dependency Review, Security Audit, and Trivy scans.

## Usage

```yaml
- name: Generate Security Summary
  uses: jdfalk/security-summary-action@v1
  if: always()
  with:
    codeql-result: ${{ needs.codeql-analysis.result || 'skipped' }}
    dependency-review-result: ${{ needs.dependency-review.result || 'skipped' }}
    security-audit-result: ${{ needs.security-audit.result || 'skipped' }}
    trivy-result: ${{ needs.trivy-scan.result || 'skipped' }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `codeql-result` | CodeQL Analysis result status | No | `skipped` |
| `dependency-review-result` | Dependency Review result status | No | `skipped` |
| `security-audit-result` | Security Audit result status | No | `skipped` |
| `trivy-result` | Trivy Scan result status | No | `skipped` |

## What It Does

- Generates a markdown summary table of all security scan results
- Writes the summary to `$GITHUB_STEP_SUMMARY` for GitHub Actions workflow summary page
- Alerts with ⚠️ if any scans report failures
- Confirms with ✅ if all scans pass or are skipped

## Example Output

```
## Security Scan Summary

| Scan Type | Status |
|-----------|--------|
| CodeQL Analysis | success |
| Dependency Review | skipped |
| Security Audit | success |
| Trivy Scan | success |

✅ **All security scans passed.**
```

## Related

- Used in [ghcommon security workflow](https://github.com/jdfalk/ghcommon/blob/main/.github/workflows/security.yml)
