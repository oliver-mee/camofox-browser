# Carried patches

Base: upstream jo-inc/camofox-browser v1.18.1.

- Local-only: CAMOFOX_ADDONS parses platform-delimited unpacked extension paths and forwards them to Camoufox. Host addons are mounted read-only, not committed or baked into the image.
- Dropped: awaited virtual-display startup; already present upstream.
- Browser deployment selection: retain existing 152.0.4 / beta.30 using explicit Docker build args. Do not use stale Makefile defaults (135.0.1 / beta.24), or silently adopt newer browser backup releases.
- Playwright: retain exact 1.60.0. Upstream lock resolves 1.62.1, which fails all three viewport resize tests with unsupported Page.setViewportSize.screenSize. Exact 1.60.0 passes all 82 e2e tests with browser 152.0.4/beta.30. pnpm lockfile is authoritative for this fork; Docker installs using pnpm 11.9.0. Upstream package-lock.json is retained for upstream comparisons only, not used in deployments.
- Host Compose/network bindings and addon payloads remain separate from source.
