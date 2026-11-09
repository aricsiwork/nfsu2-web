# NFSU2 Web fork — development roadmap

This roadmap covers the `aricsiwork/nfsu2-web` fork. The target is a polished browser release that works well on desktop and Android while preserving the original single-player game.

## Product principles

- Preserve the original NFSU2 handling, physics, career progression, rewards and economy by default.
- Keep the original PC game's save files compatible; new data must remain separate and forward-compatible.
- Treat desktop and Android as first-class targets. Prefer responsive layouts and adaptive controls over separate, divergent interfaces.
- Keep the game playable with the original keyboard/controller/touch paths; new UI must not intercept gameplay input.
- Preserve the upstream MIT license and all required credits for NFSU2Recomp, mods, translations and contributors.
- Never commit generated game code, game data, extracted assets, player logs or personal hosting details.

## Phases

### Phase 0 — baseline and safety

- [x] Verify fork access, default branch and write permissions.
- [x] Read repository contribution rules in `AGENTS.md`.
- [x] Identify the page entry point, existing CSS pipeline and responsive breakpoints.
- [ ] Run the existing TypeScript check and fast test suite in a full development environment.
- [ ] Record baseline browser/device coverage and any pre-existing failures.

**Exit criteria:** the existing build and fast tests pass, or known baseline failures are documented before feature work proceeds.

### Phase 1 — start-page UI refresh (current)

- [x] Add a separate, layered visual theme without replacing the existing page styles.
- [x] Keep the existing DOM, translations, keyboard navigation, dialogs and game controls intact.
- [ ] Review desktop, tablet, portrait phone and landscape phone layouts.
- [ ] Check contrast, focus visibility, reduced-motion behavior and long translated labels.
- [ ] Run `npm run check` and `npm run test:fast` from `web/`.

**Exit criteria:** the start page feels cohesive on desktop and Android, with no clipped controls, lost interactions or regressions in the original game flow.

### Phase 2 — responsive interaction and mobile performance

- Audit touch targets, virtual controls, orientation changes and safe-area spacing.
- Improve loading/progress feedback and low-memory device behavior without weakening capability checks.
- Verify Chrome on Android and desktop Chrome/Firefox; document WebGPU support limits by device.
- Add or update automated viewport and interaction tests where the existing harness supports them.

### Phase 3 — garage, profile and save experience

- Improve the presentation of profiles, saves, playtime and last-played information.
- Make car and tuning information easier to browse where the current game/runtime exposes it.
- Add favorites and shareable setup metadata only where it can be stored separately from stock saves.
- Keep unknown/newer save metadata intact; never overwrite a newer or unreadable save.

### Phase 4 — online and community experience

- Review current free-roam, friends, crews, lobbies and messaging before adding overlapping systems.
- Improve discoverability and feedback for joining friends, creating/joining rooms and starting races.
- Add race/player summaries and leaderboards only with clear server-side validation and abuse controls.
- Preserve offline/single-player play when online services are unavailable.

### Phase 5 — graphics and presentation

- Profile rendering before changing graphics defaults.
- Keep enhancements optional and provide sensible device-aware defaults.
- Measure frame time, memory and thermal impact on Android as well as desktop.
- Do not commit game-derived or copyrighted assets; use only properly licensed resources.

### Phase 6 — optional features

- Photo-mode improvements and replay capture, subject to browser memory and performance limits.
- Daily/community challenges that do not alter the original career economy.
- Car/setup sharing with validation and explicit import/export.
- Additional accessibility and localization improvements.

### Phase 7 — release readiness

- Run TypeScript checks, fast tests, relevant C/runtime tests and a production build.
- Test fresh install, returning player, existing saves, offline start, online reconnect and mobile rotation.
- Review license notices, credits, changelog and deployment instructions.
- Tag a release only after the release checklist passes.

## Current implementation branch

Branch: `feature/modern-start-ui`

Initial change: a new `web/src/app/modern.css` layer imported after the existing `style.css`. It refreshes the start page's color palette, panel treatment, primary Play action, stats and tabs while leaving the existing DOM and behavior in place.

## Validation commands

From `web/`:

```sh
npm ci
npm run check
npm run test:fast
npm run build
```

For runtime changes, follow the additional test/build requirements in `AGENTS.md`.
