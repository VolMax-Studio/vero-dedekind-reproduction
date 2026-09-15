# Evidence inventory

## Literal observed facts

- Vero commit: `0a7325df9e9e6dbc275c0ad483b3d1cbe38d9b09`
- Lean: `4.29.1`, `x86_64-unknown-linux-gnu`, commit
  `f72c35b3f637c8c6571d353742168ab66cc22c00`, Release
- Lake: `5.0.0-src+f72c35b` (Lean `4.29.1`)
- `lake update`: exit code `0`
- `lake exe cache get`: exit code `0`
- command under test: `lake build DedekindReals.Spec.Multiplication`
- command exit code: `1`
- command start: `2026-09-15 20:24:32.995423012 +0200`
- command completion: `2026-09-15 20:27:34.077896838 +0200`
- `git status --porcelain` after cache preparation: empty
- `git status --porcelain` after the run: empty

## Diagnostic locations

Lean reported seven `Application type mismatch` diagnostics in
`DedekindReals/Spec/Multiplication.lean`:

| Line | Argument |
| ---: | --- |
| 146 | `xNZ` |
| 153 | `xNZ` |
| 154 | `mxNZ` |
| 161 | `xNZ` |
| 169 | `xNZ` |
| 176 | `xNZ` |
| 183 | `xNZ` |

Each diagnostic reports an implementation-field proof type such as
`impl.dedekindReals.Rneq x (impl.dedekindReals.R_of_Q 0)` where the global
type `Rneq x (R_of_Q 0)` is expected by `impl.dedekindReals.Rinv`.

## Input integrity

The relevant SHA-256 values were equal before and after execution:

```text
583e3eda75a5d1bab78f4814435e5fe69acee9113d8dcf55f2ab278fee0af86e  DedekindReals/Impl/Multiplication.lean
6e74a74b48f6f1cb1e22409801e4fa36ab6b14a82bcc04f20e255a6f42d4f781  DedekindReals/Spec/Multiplication.lean
```

## Receipt mapping

| File | Meaning |
| --- | --- |
| `command.txt` | exact command under test |
| `cache_setup.txt` | dependency preparation and exit codes |
| `git_commit.txt` | exact Vero commit |
| `lean_version.txt` | literal Lean version output |
| `lake_version.txt` | literal Lake version output |
| `input_hashes.txt` | pre-run relevant source hashes |
| `input_hashes_after.txt` | post-run relevant source hashes |
| `stdout.log` | sanitized literal Lake/Lean stdout |
| `stderr.log` | literal stderr |
| `exit_code.txt` | numeric process exit code |
| `timing.txt` | receipt creation/modification timestamps |

The only changes made to `stdout.log` for publication were replacement of the
host-specific scratch checkout prefix with `$VERO_CHECKOUT` and the temporary
toolchain-home prefix with `$ELAN_HOME`. Diagnostic text, line numbers, order,
and exit status were not changed.
