# X176 Freedom

**JamesDSP Liveprog / EEL2 audio-processing script**  
Public snapshot: **X176 Freedom 1.8.41 — Warm Body v1**

X176 Freedom is the flexible parent script in the X176 line. Its default configuration is a restrained four-node “Warm Body” tuning; optional spatial and sound-editing primitives remain in the source but are not enabled by the default preset.

> **Release scope:** this repository publishes the existing 1.8.41 source snapshot and supporting public documentation. The publication and documentation corrections do not imply that every optional processing path has been tested in every host.

## Features

- Node-based processing with a configured maximum of 10 nodes (MAX_NODES = 10); the default Warm Body preset uses four.
- Parametric EQ using SVF and biquad paths.
- Dynamic shaping, harmonic generation and nonlinear waveshaping.
- Mid/Side (M/S) weighting and processing.
- Optional spatial and sound-editing buses built from primitives such as TAP, FDN, AIR and related modules; buses are disabled by default.
- Conditional bypass paths intended to avoid unnecessary work when modules are inactive.

## Compatibility

| Host | Status in this repository |
| --- | --- |
| JamesDSP Liveprog on Android | Target host; validate against the version in use |
| RootlessJamesDSP | Target host; validate independently |
| JDSP4Linux / JamesDSP for Linux | Target host; validate independently |

The table identifies intended targets, not a claim that this repository contains repeatable integration-test results for every host/version combination.

## Install

1. Download [X176_Freedom.eel](X176_Freedom.eel).
2. In a compatible JamesDSP host, open **Liveprog** and import the script.
3. Enable it and first test with the default configuration at a moderate listening level.
4. Change one parameter group at a time, keeping a copy of the unmodified script so you can revert.

## Default Warm Body tuning

The default preset is intended to gently reduce a perceived bright/thin or “papery” balance while retaining body. Its documented settings include:

- 75 Hz bell: +1.8 dB.
- Around 250 Hz: low-shelf lift of approximately +1.0 dB.
- 3.3 kHz bell: −2.0 dB.
- 6.3 kHz bell: −1.2 dB.
- Selected low-frequency nodes work on Mid only; the two upper corrective nodes use increased Side weighting.
- Output gain is reduced to leave some headroom.
- Spatial buses are disabled by default.

These are design intentions and parameter descriptions, not a guarantee that every listener or source will prefer the tuning. Perceived sound quality should be judged by listening tests with familiar material.

## Main tuning controls

The source provides four pre-gain controls in the node configuration area:

| Control | Intended role |
| --- | --- |
| PRE_BASS | Low-frequency amount |
| PRE_BODY | Low-mid body |
| PRE_MID | Midrange |
| PRE_TOP | High-frequency amount |

A value of 1.0 means the configured default amount; 0 disables that contribution. Use the source comments to locate the configuration section and keep node-setting calls before rebuild_active_list().

## Important configuration-order rules

Some examples near the end of the source are illustrative configuration snippets. Do not enable every example in place without checking its preconditions.

- **Node sends:** set_p_send(...) calls must be placed in the node configuration section, after the relevant node_begin() setup and before rebuild_active_list(). The active-node list and send-activity flag are built at initialization; configuring sends later can leave them out of date.
- **Three-bus example:** the source default is BUS_MAX = 2, so only bus IDs 0 and 1 are available. The example labelled “three-band processing” uses bus ID 2; that example requires BUS_MAX >= 3 before the script is loaded. With the default value, the helper clamps bus ID 2 to bus 1, where it can overwrite that bus's configuration. Increasing the bus count also changes memory and processing requirements; re-test before use.
- **Finalize last:** spatial-bus configuration calls must be placed before s_finalize(), which finalizes configured bus state.

The public script's inline warnings are the source of truth for exact call order and parameter constraints.

## Performance estimate

The source documents approximately **1.25k weighted operation units per sample** for the default Warm Body configuration. This is a static, weighted estimate intended for relative comparison—not a measured CPU percentage, wall-clock benchmark, or promise of performance across devices and hosts. Actual load depends on host, sample rate, build/runtime and the enabled processing path.

## Repository contents

- X176_Freedom.eel — the Liveprog script.
- README.md — overview, install notes and important configuration constraints.
- CHANGELOG.md — public release and documentation-change record.
- TESTING.md — current validation scope and recommended checks.
- CONTRIBUTING.md — maintenance and review checklist.
- LICENSE — MIT License.

The internal maintainer scripts mentioned in the source history are not included here. Therefore, their previous results should not be treated as automatically reproducible from this repository alone.

## License

[MIT License](LICENSE).
