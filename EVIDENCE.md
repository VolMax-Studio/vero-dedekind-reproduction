# Execution evidence

## Identity

- Vero commit: `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`
- Lean: `4.29.1` (`f72c35b3f637c8c6571d353742168ab66cc22c00`)
- Lake: `5.0.0-src+f72c35b`
- target: `DedekindReals.Spec.Multiplication`
- build exit code: `1`

## Input integrity

Before execution:

```text
583e3eda75a5d1bab78f4814435e5fe69acee9113d8dcf55f2ab278fee0af86e  DedekindReals/Impl/Multiplication.lean
6e74a74b48f6f1cb1e22409801e4fa36ab6b14a82bcc04f20e255a6f42d4f781  DedekindReals/Spec/Multiplication.lean
```

After execution the two hashes were identical. Git porcelain status was empty after dependency preparation and after the target build.

## Literal Lean diagnostics

The build reached `DedekindReals.Spec.Multiplication` and returned seven `Application type mismatch` diagnostics:

```text
DedekindReals/Spec/Multiplication.lean:146:35
DedekindReals/Spec/Multiplication.lean:153:58
DedekindReals/Spec/Multiplication.lean:154:59
DedekindReals/Spec/Multiplication.lean:161:61
DedekindReals/Spec/Multiplication.lean:169:61
DedekindReals/Spec/Multiplication.lean:176:59
DedekindReals/Spec/Multiplication.lean:183:61
```

Representative diagnostic, reproduced verbatim:

```text
Application type mismatch: The argument
  xNZ
has type
  impl.dedekindReals.Rneq x (impl.dedekindReals.R_of_Q 0)
but is expected to have type
  Rneq x (R_of_Q 0)
in the application
  impl.dedekindReals.Rinv x xNZ
```

The final Lean/Lake messages were:

```text
error: Lean exited with code 1
Some required targets logged failures:
- DedekindReals.Spec.Multiplication
error: build failed
```

## Timing

- start: `2026-09-15 20:24:32 +0200`
- completion: `2026-09-15 20:27:34 +0200`

The local evidence custody record retains the complete unfiltered stdout/stderr. This public record omits temporary scratch paths and host-specific system metadata because they are not required to reproduce or evaluate the finding.
