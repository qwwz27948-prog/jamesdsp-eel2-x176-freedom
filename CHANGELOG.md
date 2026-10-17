# Changelog

This file records public repository releases and changes visible to repository users. It is not a replacement for the project's internal review logs.

## 2026-10-17 — Public snapshot: X176 Freedom 1.8.41 Warm Body v1

- Published the existing X176 Freedom 1.8.41 Warm Body source snapshot as X176_Freedom.eel.
- The default configuration uses four nodes and leaves spatial buses disabled.
- The public source retains optional spatial and sound-editing primitives.
- The initial publication includes a README and MIT license.

### Configuration caveats identified during public-source review

These caveats also appear in the maintained source snapshot from before publication; they are documented here to prevent misuse and are not attributed to the act of publishing the file.

- The three-band example uses bus IDs 0, 1 and 2 while the default BUS_MAX is 2 (valid IDs: 0 and 1). Use that example only after increasing BUS_MAX to at least 3 and revalidating memory and performance.
- set_p_send() must run before rebuild_active_list() and the send-activity scan. The send example near the end of the source must be moved to the earlier node configuration area before it is enabled.

## 2026-10-17 — Public documentation and example-safety review

- Clarified target-host status, default node count, performance-estimate scope and configuration ordering in the README.
- Added a testing checklist and contributor checklist.
- Added inline warnings to the example snippets for the two configuration-order/capacity constraints above.
- These changes are limited to documentation/comments; they do not intentionally alter the active DSP processing expressions. Native EEL2 host compilation and audio integration testing remain necessary.
