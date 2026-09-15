# Vero DedekindReals reproduction

Independent verification by **VolMax Studio Lab** of a frozen-specification
elaboration failure in Vero.

## Result

**`FAIL_MATCH — independently execution-reproduced`**

- Vero commit: `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`
- Lean toolchain: `v4.29.1`
- command under test: `lake build DedekindReals.Spec.Multiplication`
- observed exit code: `1`

The frozen `DedekindReals.Spec.Multiplication` module does not elaborate under
the released commit and pinned toolchain. Lean reports seven
`Application type mismatch` diagnostics involving the
`RinvSig / Rneq / R_of_Q` boundary before candidate proof search.

This artifact establishes that narrow build-level failure. It does **not**
claim that the complete published `0/82` score is proven to be exclusively
caused by this defect.

## Contents

- [`REPRODUCTION.md`](REPRODUCTION.md) defines the frozen question, procedure,
  acceptance criteria, result, and limitations.
- [`EVIDENCE.md`](EVIDENCE.md) inventories the observed execution facts.
- [`evidence/run-001/`](evidence/run-001/) contains sanitized execution
  receipts. It does not contain Vero source code.

## Prior report / provenance

This was an independent reproduction, not the original discovery. The initial
failure report was published in
[sunblaze-ucb/vero issue #4](https://github.com/sunblaze-ucb/vero/issues/4).
VolMax Studio Lab independently executed and adjudicated the frozen experiment
recorded here.
