# Reproduction protocol and result

## Question under test

At Vero commit `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`,
using the repository-pinned Lean toolchain, does the frozen module
`DedekindReals.Spec.Multiplication` elaborate successfully before candidate
proof search?

## Frozen environment

- repository: `sunblaze-ucb/vero`
- Git commit: `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`
- Lean: `4.29.1`, commit
  `f72c35b3f637c8c6571d353742168ab66cc22c00`, Release
- Lake: `5.0.0-src+f72c35b` (Lean `4.29.1`)
- Git working tree before execution: clean
- relevant source files: unchanged before and after execution

Vero source is not vendored in this artifact. Obtain it from the upstream
repository and detach the checkout at the exact commit above.

## Dependency preparation

From `benchmarks/DedekindReals` in the pinned checkout:

```bash
lake update
lake exe cache get
```

Both commands returned exit code `0`. This uses Vero's normal mathlib cache
path and avoids treating a full local source compilation of mathlib as part of
the scientific question.

## Exact command

```bash
lake build DedekindReals.Spec.Multiplication
```

## Acceptance criteria

- **PASS:** exit code `0`.
- **FAIL_MATCH:** nonzero exit code with an `Application type mismatch`
  involving `RinvSig / Rneq / R_of_Q` in the frozen multiplication
  specification.
- **FAIL_OTHER:** nonzero exit code caused by a different failure, including
  toolchain, dependency, or infrastructure failure.

The criteria were fixed before the completed execution.

## Observed result

The command returned exit code `1`. Lean emitted seven
`Application type mismatch` diagnostics at lines 146, 153, 154, 161, 169,
176, and 183 of `DedekindReals/Spec/Multiplication.lean`. The diagnostics show
that proofs formed with the arbitrary implementation's `Rneq` and `R_of_Q`
fields are supplied where the global `Rneq` and `R_of_Q` proof type is
expected by `Rinv`.

The Git working tree remained clean and the two relevant source-file SHA-256
hashes were identical before and after execution.

## Adjudication

**`FAIL_MATCH — independently execution-reproduced`**

The observed exit code and literal diagnostic signature match the frozen
`FAIL_MATCH` criterion.

## Scope limitations

This reproduction establishes the frozen-module elaboration failure before
candidate proof search. It does not:

- prove that all 82 published DedekindReals failures share this sole cause;
- execute the complete official scoring pipeline;
- evaluate any other Vero benchmark;
- call an AI model; or
- claim original discovery of the defect.
