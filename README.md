# Reproduce Next 16.2.6 TypeScript 7 RC build failure

Minimal reproduction for `next build` failing when `typescript@7.0.1-rc` is installed as `typescript`.

## Versions

- Next.js: `16.2.6`
- TypeScript: `7.0.1-rc`
- Package manager: Bun

## Reproduce

```bash
bun install --frozen-lockfile
CI=1 bun run build
```

Expected: Next.js builds successfully or reports a clear TypeScript 7 compatibility message.

Actual: Next.js compiles successfully, prints `Skipping validation of types`, then exits with code 1 during TypeScript setup even though `typescript@7.0.1-rc` is installed.

Without `CI=1`, Next.js attempts to auto-install `typescript` with another package manager, which mutates the install instead of surfacing the incompatibility.
