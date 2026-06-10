# NSGminer - Project Brief

## Project Overview

NSGminer is a high-performance, multithreaded multipool cryptocurrency mining software supporting GPU (AMD/NVIDIA), CPU, and FPGA (BitForce, Icarus, ModMiner, X6500, ZTEX) mining operations. It provides advanced device monitoring, automated overclocking/fan control, and a comprehensive RPC API for remote management.

**Purpose:** Provide miners and mining farm operators with a robust, feature-rich mining solution that maximizes hardware efficiency while maintaining stability and ease of use.

**Target Audience:** Cryptocurrency miners, mining pool operators, and mining farm administrators.

**Key Features:**
- Multi-algorithm support: NeoScrypt, Scrypt, SHA-256d
- GPU mining with AMD (OpenCL via ADL) and NVIDIA (NVML) monitoring/control
- CPU mining with multiple optimized SHA-256 implementations
- FPGA mining with autodetection and bitstream management
- Multipool support with multiple failover strategies (failover, round-robin, rotate, load balance, balance)
- Advanced thermal management: auto-fan, auto-gpu with temperature targeting
- RPC API for remote monitoring and control
- Text-based UI with real-time statistics and hotkey configuration
- Solo mining support via GBT-compatible nodes

**Technology Stack:**
- C language (performance-critical codebase)
- GNU Autotools build system (autoconf, automake, libtool)
- OpenCL for GPU computation
- ADL (ATI Display Library) for AMD GPU monitoring/control
- NVML for NVIDIA GPU monitoring
- libusb for FPGA device communication
- curses/ncurses for terminal UI
- JSON-RPC over HTTP for API

**License:** GPLv3

---

## Important: Local-Only Volatile Memory

**This entire `.kilocode/rules/memory-bank/` directory contains local-only, volatile memory that is NOT committed to the repository.** The memory bank serves as session-scoped context for AI agents and is noncanonical.

**For authoritative, permanent documentation, always refer to:**
- [`docs/maintainer-wiki/index.md`](../docs/maintainer-wiki/index.md) - Canonical maintainer wiki
- [`AGENTS.md`](../AGENTS.md) - Repository policy and agent guidelines

Any technical facts, decisions, or procedures that need to persist must be stored in the maintainer wiki, not in this memory bank.

---

## Project Context (from Evidence)

**Build System:** GNU Autotools (`./autogen.sh && ./configure && make`)
**Configure Options:** Extensive algorithm and hardware feature flags (see `README:57-74`)
**Configuration:** JSON config file + command-line arguments
**API Port:** 4028 (default)
**RPC API:** Documented in `API-README`
**FPGA Bitstreams:** Included in `bitstreams/` directory
**Submodules:** Git submodules used for third-party code

**Evidence Sources:**
- [`README`](../README) - Primary user documentation (1,016 lines)
- [`AGENTS.md`](../AGENTS.md) - Agent entrypoint and repository policy
- [`docs/maintainer-wiki/workflows.md`](../docs/maintainer-wiki/workflows.md) - Build/test/deploy procedures
- [`configure.ac`](../configure.ac) - Build configuration and feature detection
- [`example.conf`](../example.conf) - Sample configuration

---

## Canonical vs. Noncanonical

| Type | Source | Authority | Mutability |
|------|--------|-----------|------------|
| Protocol parameters | Source code (`chainparams.cpp` equivalent) | Canonical | Immutable |
| Build procedures | [`docs/maintainer-wiki/workflows.md`](../docs/maintainer-wiki/workflows.md) | Canonical | Versioned |
| API contracts | [`API-README`](../API-README) | Canonical | Versioned |
| Runtime defaults | [`miner.c`](../miner.c), [`example.conf`](../example.conf) | Canonical | Versioned |
| Agent task context | `.kilocode/rules/memory-bank/` | **Noncanonical** | Volatile |
| Session notes | `.kilocode/rules/memory-bank/` | **Noncanonical** | Volatile |

**Code wins over documentation.** If a discrepancy is found, trust the implementation, then update canonical docs.
