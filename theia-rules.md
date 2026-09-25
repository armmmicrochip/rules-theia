---
paths:
  - "**/.theia/**"
  - "**/*-frontend-module.ts"
  - "**/*-backend-module.ts"
  - "**/src/browser/**/*.{ts,tsx}"
  - "**/src/node/**/*.ts"
  - "**/src/common/**/*.ts"
  - "**/src/electron-*/**/*.{ts,tsx}"
  - "**/src/node-electron/**/*.ts"
---

# Theia project rules
- Theia code detected. Invoke the `theia` skill before writing DI, contribution, or RPC code.
- Terse output: code plus ≤2 lines of rationale. No filler, no summaries of what was done.
- Minimal reads: open only the files being edited and the type definitions they consume. Skip node_modules (except a targeted grep of `@theia/*/src` for a symbol), lib/, src-gen/, gen-webpack*.
- Public services: symbol + interface + `@injectable` impl, bound with `toSelf().inSingletonScope()` + `toService`. Injected fields are `protected readonly`.
- Platform folders: `common` has no DOM and no Node. `browser` and `electron-browser` have DOM but no Node. `node` and `node-electron` have Node but no DOM. `browser` and `node` never import each other.
- React: import only from `@theia/core/shared/react` or `@theia/core/shared/react-dom`, never from `react` directly. React 19 only.
- User-facing strings: `nls.localize('ext/key', 'Default {0}', arg)`; commands via `Command.toLocalizedCommand`. No hardcoded UI text.
- Frontend and backend have separate DI containers and may run on different hosts. Share code only through `common` and exchange data only via RPC.
