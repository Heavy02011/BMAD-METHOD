# Security Vulnerability Report - glob Package

## Summary

Updated the `glob` package from version 11.0.3 to 11.1.0 to address a critical command injection vulnerability.

## Vulnerability Details

### Primary Vulnerability (FIXED ✅)

- **Package**: glob
- **Affected Versions**: >= 11.0.0, < 11.1.0
- **CVE**: GHSA-5j98-mcp5-4vw2
- **Severity**: High (CVSS 7.5)
- **Issue**: Command injection via -c/--cmd executes matches with shell:true
- **Fix**: Updated to version 11.1.0

### Secondary Vulnerability (FIXED ✅)

- **Package**: glob (transitive via jest)
- **Affected Versions**: >= 10.2.0, < 10.5.0
- **Fix**: Updated to version 10.5.0 via npm audit fix

## Changes Made

### Direct Dependencies

- ✅ Updated `glob` from `^11.0.3` to `^11.1.0` in package.json
- ✅ Ran `npm install` to update package-lock.json
- ✅ Ran `npm audit fix` to update fixable transitive dependencies

### Transitive Dependencies Status

- ✅ **jest dependencies**: Updated to glob@10.5.0 (patched)
- ⚠️ **semantic-release → npm**: glob@10.4.5 (bundled, requires breaking change to fix)

## Remaining Vulnerability

One vulnerability remains in a bundled dependency:

```
glob@10.4.5 (bundled in npm@10.9.4 within semantic-release@24.2.7)
```

### Why It Wasn't Fixed

- This glob version is bundled within the `npm` package
- The `npm` package is a dependency of `@semantic-release/npm`
- Fixing requires upgrading `semantic-release` from 24.2.7 to 25.0.3
- This is a **MAJOR version change** with potential breaking changes

### Recommendation

Consider upgrading semantic-release to v25 in a separate PR after:

1. Reviewing the semantic-release v25 changelog
2. Testing the release workflow
3. Ensuring compatibility with current configuration

### Risk Assessment

The remaining vulnerability has **LOW risk** in this context because:

- It's in the CLI functionality of glob (--cmd flag)
- semantic-release/npm uses glob programmatically, not via CLI
- The vulnerability requires specific CLI usage patterns that aren't present in this codebase

## Verification

To verify the fixes:

```bash
# Check direct glob version
npm list glob --depth=0

# Check all glob versions
npm list glob

# Run security audit
npm audit
```

## References

- GitHub Advisory: https://github.com/advisories/GHSA-5j98-mcp5-4vw2
- glob package: https://www.npmjs.com/package/glob
- semantic-release: https://github.com/semantic-release/semantic-release

---

**Date**: 2026-02-05  
**Fixed by**: GitHub Copilot Workspace Agent
