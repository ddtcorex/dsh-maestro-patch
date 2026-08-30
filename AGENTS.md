# AGENTS.md — dsh-maestro-patch

> `CLAUDE.md` is a symlink to `AGENTS.md`.

## Purpose

Zero-fork shim for `ddtcorex/deepseek-harness` fork patches. Reproduces 5 runtime patches via reversible Cordis effects so `deepseek-harness` can track `upstream` verbatim.

| Patch | Origin | Shim |
|---|---|---|
| viewport maximum-scale=1 | `30a315c` | `src/client/patches/viewport.ts` |
| apple-touch-icon | `671699c` | `src/client/patches/apple-icon.ts` + `assets/` |
| __DSH_TRUSTED_PROXY__ → isLoopback | `ad539de` | `src/client/patches/connection.ts` |
| BlockAssembler keepBlock | `9bbc985` | `src/host/patches/assembler.ts` |
| welcome-store localStorage | `59b8783` | `src/client/patches/welcome.ts` |

All shims are `ctx.effect` reversible and feature-detect upstream.

## Layout

- `src/host/` — host patch (assembler)
- `src/client/` — client patches (viewport, apple-icon, connection, welcome)
- `assets/apple-touch-icon.png` — 180x180
- `cordis.patch.yml` — id `maestro-patch` inject `['connection']`
- `scripts/build-client.mjs` — wraps CommonJS emit into `lib/client.js` via `__ModuleLoader__`

## Development

```sh
pnpm verify
pnpm test
pnpm build
```

## Git workflow

- Default branch `master`, Conventional Commits, PR required, `verify` check.
- Release via `git tag vX.Y.Z && git push origin vX.Y.Z` (reusable `dsh-maestro-ci`).

