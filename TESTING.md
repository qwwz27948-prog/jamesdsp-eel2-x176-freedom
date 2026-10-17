# Testing and validation

## Current verification status

This repository does **not** currently include the internal maintenance toolchain or a host-independent automated test runner. The presence of a script in the repository is not, by itself, proof that it compiles or behaves correctly in every EEL2 host.

The public-source review for the documentation update checked the relevant configuration declarations and example ordering. It did not run a JamesDSP/Liveprog host, measure device CPU use, or perform listening tests. Do not interpret this documentation update as a runtime certification.

## Recommended validation layers

### 1. Static source checks

- Check EEL2 syntax and function declaration/call order using the target host or a validated EEL2 checker.
- Check array and memory-pool bounds, indices and all configuration clamp paths.
- Check that the single-channel, Mid and Side engine mirrors remain consistent where the source documents them as mirrors.
- Check every configuration example against MAX_NODES, BUS_MAX, stage limits and its required call order.
- Confirm all node setup and set_p_send() calls occur before rebuild_active_list(); confirm bus setup is complete before s_finalize().

### 2. State and numerical checks

- Validate initialization, reset behavior and state persistence across repeated processing calls.
- Exercise silent input, full-scale sine, full-scale noise, impulses, decays, and parameter boundary values.
- Test sample-rate changes and maximum supported settings for delay and spatial primitives.
- Check that output remains finite and that feedback systems remain bounded under supported parameter limits.

### 3. Signal regression checks

- Compare the default Warm Body output against a declared baseline using fixed input samples, sample rate, host/runtime and parameter set.
- Test Mid-only, Side-only and dual-channel node paths, plus changes to each PRE_* control.
- Test spatial buses disabled and enabled separately.
- If claiming bit-identical output, use a reproducible sample-by-sample comparison; comments or matching formulas alone are insufficient.

### 4. Host integration and performance

- Import the script in each target host/version and confirm it initializes without a parse/import error.
- Verify audible output, bypass behavior, channel handling, preset changes and parameter changes.
- Measure CPU/runtime cost on a named device, sample rate, buffer configuration and exact processing setup. Do not present the source's weighted “units/sample” estimate as a measured CPU percentage.
- Listen to familiar reference material at matched loudness; objective numerical tests do not establish subjective preference.

## Test-report template

For each test run, record:

- Script commit SHA and file hash.
- Host/app version, device/OS and audio route.
- Sample rate and relevant buffer/configuration values.
- Exact preset and parameter changes.
- Input fixture and duration.
- Tool/command and pass/fail result.
- For audio comparison: maximum absolute error, RMS error and any criteria used.
- Known failures, warnings and untested paths.

Internal tools such as the EEL lint, persistence checker and hotspot profiler may help maintainers, but they are not distributed here. A public test report should identify which tools actually ran and include enough detail for another maintainer to reproduce the result.
