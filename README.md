# dsh-maestro-patch

Zero-fork shim for `ddtcorex/deepseek-harness` customizations. Reproduces the 5 runtime patches from the fork via reversible Cordis effects so `deepseek-harness` can track `upstream` verbatim.

| Patch | Origin | Shim location |
|---|---|---|
| `viewport maximum-scale=1` | `30a315c` | `src/client/patches/viewport.ts` |
| `apple-touch-icon` | `671699c` | `src/client/patches/apple-icon.ts` + `assets/apple-touch-icon.png` + host fallback |
| `__DSH_TRUSTED_PROXY__` → `isLoopback` | `ad539de` | `src/client/patches/connection.ts` (after `connection` mount) |
| `BlockAssembler keepBlock + tool-call id/name restore` | `9bbc985` + plugin-only | `src/host/patches/assembler.ts` |
| `welcome-store localStorage` | `59b8783` | `src/client/patches/welcome.ts` |

All shims are `ctx.effect` reversible and feature-detect upstream (no-op when upstream already contains the fix).

Validate on ephemeral profile/port before live: `DSH_HOME=$(mktemp -d) dsh web --port <ephemeral> --profile ephemeral-patch-test`.

## Development

```sh
pnpm verify
pnpm test
pnpm build
```
