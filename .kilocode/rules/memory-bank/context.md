# Project Context

**Status:** Wiki initialization complete; codebase analyzed and understood.
**Last Updated:** 2025-06-10
**Volatility:** This file contains local-only, volatile, and noncanonical context. Authoritative facts are in [`docs/maintainer-wiki/index.md`](../../docs/maintainer-wiki/index.md).

## Current State

The NSGminer repository has a well-established maintainer wiki in `docs/maintainer-wiki/` with:

- **Workflows** (`workflows.md`): Complete build, test, and deployment procedures for Linux/macOS/Windows (with gaps noted)
- **Tech Stack** (`tech-stack.md`): Evidence-backed inventory of tools and dependencies
- **Open Work** (`open-work.md`): Tracked unresolved tasks and known gaps (see below)
- **Architecture** (`concept-architecture-overview.md`): System component map
- **Decision Log** (`decisions.md`): Historical rationale record
- **Agent Guide** (`agent-guide.md`): Operating notes for maintainers
- **Canonical Sources** (`reference-canonical-sources.md`): Source-of-truth hierarchy

The wiki is functional but has identified documentation gaps that need attention.

## Recent Actions

- Initialized memory bank directory structure
- Reviewed main documentation sources: `README`, `AGENTS.md`, `docs/maintainer-wiki/workflows.md`
- Analyzed `open-work.md` for prioritized task awareness
- Created `brief.md` with project summary and scope

## Next Steps

Immediate next actions based on open work items:

1. **Address Windows build documentation gap** - `open-work.md` flag: "Windows Build Instructions Missing" (High Priority)
   - Option A: Create `windows-build.txt` as referenced in `README:109`
   - Option B: Expand Windows section in `workflows.md` to be comprehensive

2. **FPGA bitstream compatibility verification** - `open-work.md` flag: "FPGA Bitstream Compatibility Verification" (High Priority)
   - Create mapping of bitstream versions (`bitstreams/*.bit`) to hardware revisions
   - Document recommended defaults and verification procedure

3. **AMD APP SDK version recommendations update** - `open-work.md` flag: "AMD APP SDK Version Recommendations" (High Priority)
   - Research current ROCm compatibility
   - Update guidance for GCN and newer architectures
   - Clarify if SDK 2.4/2.5 recommendations are still valid or obsolete

4. **API version deprecation policy** - `open-work.md` flag: "API Version Deprecation Tracking" (Medium Priority)
   - Define supported API versions (v0.7–v1.24 range documented)
   - Add compatibility matrix to `workflows.md` or create `api-support-policy.md`

5. **Security best practices guide** - `open-work.md` flag: "Security Considerations for RPC API" (Medium Priority)
   - Consolidate `--api-allow`, `--api-groups`, network controls
   - Document secure deployment patterns in `workflows.md` or new `security.md`

## Open Questions

- Are there automated tests? `workflows.md` mentions `make check` but existence unclear from current scan.
- Release signing procedures: Does `make-release` include GPG signatures or checksums?
- CPU mining status: Marked as deprecated in `README`; should be explicitly documented in `tech-stack.md` as such.

## Dependencies and External Factors

- SDK version compatibility impacts GPU mining performance significantly (per `README` FAQ)
- FPGA autodetection depends on `libudev` and `sysfs` availability (Linux-specific)
- Windows build requires MSYS2/MinGW-w64 environment and proprietary driver/SDK installations
- OpenCL platform selection (`--gpu-platform`) needed when multiple SDKs installed

---

**Note:** This context file is for AI agent/session use only. Do not treat as canonical reference. Update canonical documentation in `docs/maintainer-wiki/` with verified facts.
