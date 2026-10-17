# Contributing

X176 Freedom is a configurable DSP script. Changes should preserve its flexible parent-version role and should not silently turn optional functionality into a mandatory processing path.

## Before changing the script

1. Identify whether the change affects active DSP expressions, initialization/configuration, documentation, or only comments.
2. Read the relevant source comments for EEL2/Liveprog parsing constraints, state layout, limits and ordering requirements.
3. For processing-engine changes, check all documented engine mirrors. The source describes three corresponding paths: the atomic single-channel engine and the Mid and Side portions of the dual engine. Update or regenerate all applicable copies consistently.
4. Check memory use and per-sample cost, especially when changing node counts, bus counts, delay pools or primitive limits.
5. Do not infer that a change is bit-identical or acoustically neutral from algebra alone. Run the corresponding regression test before making that claim.

## Configuration invariants

- Keep node setup and set_p_send() calls before rebuild_active_list().
- Finish spatial-bus configuration before s_finalize().
- A bus ID must be in the range 0 .. BUS_MAX - 1. Check examples whenever BUS_MAX changes.
- Keep spatial modules disabled by default unless a deliberate, reviewed preset change is intended.
- Distinguish static operation-cost estimates from measurements taken on a real host/device.

## Before proposing a change

- State the user-visible behavior or defect being addressed.
- Keep unrelated formatting and algorithm changes out of the same change when possible.
- Include the exact checks run and the environment used.
- List limitations and untested paths explicitly.
- For documentation-only changes, say so; do not imply the DSP engine has been revalidated.

## Suggested review checklist

- [ ] Active DSP expressions are unchanged unless the change explicitly requires otherwise.
- [ ] Initialization order and configuration snapshots were reviewed.
- [ ] Single/Mid/Side engine paths remain consistent.
- [ ] Memory indices, clamps and maximum settings were checked.
- [ ] Documentation examples match the current limits and call order.
- [ ] Test claims have reproducible evidence.
- [ ] The changelog describes the change without attributing prior work to the publication step.
