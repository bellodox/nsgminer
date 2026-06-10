# Active Tasks and Known Issues

**Status:** Wiki initialization complete; development environment ready.
**Last Updated:** 2025-06-10
**Volatility:** This file contains local-only, volatile, and noncanonical task tracking. Authoritative task tracking is in [`docs/maintainer-wiki/open-work.md`](../../docs/maintainer-wiki/open-work.md).

## Active Tasks

No immediate active tasks. The memory bank and maintainer wiki have been successfully initialized. The project is ready for normal development workflows.

## Known Issues and Gaps

The following issues are tracked in the canonical [`open-work.md`](../../docs/maintainer-wiki/open-work.md) and require attention:

### High Priority

1. **Windows Build Instructions Missing**
   - Missing `windows-build.txt` file referenced in `README:109`
   - Windows build section in `workflows.md` needs expansion

2. **FPGA Bitstream Compatibility Verification**
   - Need mapping of bitstream versions to hardware revisions
   - Missing recommended default and verification procedure

3. **AMD APP SDK Version Recommendations Update**
   - Current SDK guidance (2.4/2.5) may be outdated
   - Need ROCm/GCN compatibility information

4. **CPU Mining Deprecation Status**
   - `README` indicates CPU mining deprecated but still present in source
   - Need official deprecation timeline or removal plan

### Medium Priority

5. **API Version Deprecation Tracking**
   - API versions v0.7–v1.24 documented but support policy unclear
   - Need compatibility matrix and deprecation timeline

6. **Security Best Practices Guide**
   - RPC API security controls exist (`--api-allow`, `--api-groups`) but not consolidated
   - Need secure deployment documentation

7. **Test Coverage Documentation**
   - Unclear if automated tests exist
   - Document `make check`/`make test` procedures if present

### Low Priority

8. **Code Signing and Release Integrity**
   - No visible release signing infrastructure
   - Need checksum/GPG verification documentation

9. **Performance Tuning Guide**
   - Tuning advice scattered in `README` FAQ
   - Need consolidated optimization guide

10. **Continuous Integration Status**
    - No CI configuration visible
    - Consider implementing basic CI

---

**Note:** This file is for AI agent/session task tracking only. It is local-only, volatile, and noncanonical. For the authoritative list of open work items and their full descriptions, always refer to [`docs/maintainer-wiki/open-work.md`](../../docs/maintainer-wiki/open-work.md).
