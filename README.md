# Vero DedekindReals — Independent Reproduction

Independent reproduction by **VolMax Studio Lab** of the frozen-spec elaboration failure reported by `mohitunplugged` in [`sunblaze-ucb/vero#4`](https://github.com/sunblaze-ucb/vero/issues/4).

## Status

**`FAIL_MATCH — independently execution-reproduced`**

This status applies only to one narrow question: does `DedekindReals.Spec.Multiplication` elaborate successfully at the released Vero commit and pinned Lean toolchain?

It does **not** establish that the complete published `0/82` result for DedekindReals is caused exclusively by this defect.

## Pinned target

- Upstream: `sunblaze-ucb/vero`
- Commit: `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`
- Lean: `4.29.1`
- Lake: `5.0.0-src+f72c35b`
- Target: `benchmarks/DedekindReals`

## Reproduction

```bash
lake update
lake exe cache get
lake build DedekindReals.Spec.Multiplication
```

Observed build result: exit code `1`, with seven `Application type mismatch` diagnostics at lines 146, 153, 154, 161, 169, 176, and 183 of `DedekindReals/Spec/Multiplication.lean`, matching the `RinvSig / Rneq / R_of_Q` mismatch reported in issue #4.

The public evidence bundle is under [`evidence/run-001/`](evidence/run-001/). No Vero or other upstream source code is vendored here.

## Public record

The reproduction was reported back to Vero issue #4 on 15 September 2026:

https://github.com/sunblaze-ucb/vero/issues/4#issuecomment-5686455880

## Attribution

The defect was publicly reported first by `mohitunplugged`. This repository records an **independent reproduction** of that report and does not claim discovery priority.
