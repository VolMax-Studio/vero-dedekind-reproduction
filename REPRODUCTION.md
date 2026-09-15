# Reproduction record

## Question under test

Does the frozen module `DedekindReals.Spec.Multiplication` elaborate successfully on Vero commit `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09` under Lean `4.29.1`?

## Preconditions

- clean checkout at the pinned Vero commit
- Lean `4.29.1`
- dependency preparation through Vero's normal mathlib cache path
- no modification of the relevant Vero source files

Dependency preparation:

```bash
lake update
lake exe cache get
```

Both commands exited `0`.

## Frozen command

```bash
lake build DedekindReals.Spec.Multiplication
```

## Observed result

- exit code: `1`
- seven `Application type mismatch` diagnostics
- locations: 146, 153, 154, 161, 169, 176, 183
- mismatch class: bundle-local `impl.dedekindReals.Rneq` / `impl.dedekindReals.R_of_Q` proofs supplied to an `RinvSig` closed over global `Rneq` / `R_of_Q`
- Git porcelain status remained empty after dependency setup and after the target build
- the two relevant source hashes were identical before and after execution

The literal Lean output is preserved in `evidence/run-001/stdout.log`; Lake's final build summary is in `stderr.log`.

## Adjudication

`FAIL_MATCH — independently execution-reproduced`

The observed failure matches the command, toolchain, error class, and seven source locations described in Vero issue #4.

## Boundary

This run establishes a build-level failure in the frozen specification module before candidate proof search. It does **not**, by itself, establish that this defect is the exclusive cause of the complete published DedekindReals `0/82` score.

No FLoCq target, Verdict target, full-corpus evaluation, or model call was executed as part of this reproduction.
