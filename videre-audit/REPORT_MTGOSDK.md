# MTGOSDK — Technical Findings & Recommendations

Scope: C#/.NET SDK for interfacing with MTGO client memory. Sources reviewed include `README.md`, Win32 interop files, process utilities, and injection helpers.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Uses ClrMD to inspect managed heap objects inside MTGO process (README lines 42–46).
- Win32 interop present for process/memory ops:
  - `OpenProcess`, `ReadProcessMemory`, `VirtualAllocEx`, `CreateRemoteThread` (e.g., `MTGOSDK.Win32/src/API/Kernel32/...`).
  - Token ops via `advapi32` (`OpenProcessToken`, `AdjustTokenPrivileges`).
- SafeHandle usage exists in some helpers (e.g., `ToolHelpHandle : SafeHandleZeroOrMinusOneIsInvalid`).

## Strengths
- Clean separation of Win32 interop in `MTGOSDK.Win32` with explicit DllImports.
- Documentation is high quality and legally contextualized (DMCA interoperability, EULA note).
- MSBuild package generation and centralized props indicate good release hygiene.

## Risks / issues
- Memory/handle safety: not all interop sites clearly wrap OS handles in SafeHandle; potential leaks or double-close in error paths.
- P/Invoke attributes consistency: some functions miss `SetLastError=true` or explicit `CallingConvention`, which can hinder diagnostics.
- Privilege handling: token elevation code paths exist; lack of explicit least‑privilege policy and rollback.
- Observability: no standardized structured logging/ETW across hot paths.
- Testing: limited evidence of unit/integration tests for Win32 boundary; hard to prevent regressions across MTGO updates.

## Recommendations (prioritized)
1) Handle safety and diagnostics
- Enforce SafeHandle wrappers for all native handles (process/thread/snapshot). Add finalizers only as a backup; prefer SafeHandle lifetime.
- Ensure `SetLastError=true` on all DllImports that expose Win32 error; wrap calls with `Marshal.GetLastWin32Error()` and classify errors.

2) Privilege and hardening
- Introduce a single elevation module with explicit least-privilege scopes and auto-rollback; document when/why elevation is required.
- Add tamper‑aware guards (e.g., deny if unexpected process name/window class) to reduce misuse vectors.

3) Observability and perf
- Add structured logging (EventSource/NLog/Serilog) with correlation IDs; include last Win32 error on failures.
- BenchmarkDotNet suite for: memory scan, pointer walking, object projection. Track allocs/GC and CPU.

4) Compatibility and tests
- Golden integration tests against MTGO mock/snapshots; simulate process restarts and different bitness.
- CI on Windows runners: build + minimal smoke tests of interop calls against a stub process.

## Quick wins (1 week)
- Audit all DllImports: add/verify `SetLastError`, `ExactSpelling`, `CharSet`, `CallingConvention`.
- Wrap raw IntPtr handles in SafeHandle for: process, thread, snapshot, toolhelp.
- Add a central `Win32Error` helper to map common error codes to actionable messages.
- Introduce basic EventSource provider with INFO/WARN/ERROR for interop boundaries.

## Suggested PRs
- PR1: "Interop hardening": SafeHandle adoption + DllImport attribute review.
- PR2: "Diagnostics": add EventSource logger + Win32 error mapping.
- PR3: "Benchmarks": initial BenchmarkDotNet project with 3 hot-path benches.
