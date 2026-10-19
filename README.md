# Renovate drops pnpm's `minimumReleaseAgeExclude` prune

Minimal reproduction: with `minimumReleaseAgeExcludePrune: true`, `pnpm install` removes `minimumReleaseAgeExclude` entries the lockfile no longer resolves. Renovate runs that install but only commits `pnpm-lock.yaml`, so the `pnpm-workspace.yaml` change is lost.

- `pnpm-workspace.yaml` exempts `is-number@6.0.0`, like a Renovate security update would.
- Renovate bumps `is-number` to 7.0.0, so the exemption becomes stale.
- CI runs `pnpm install`, which prunes the entry, and `git diff --exit-code` fails.
