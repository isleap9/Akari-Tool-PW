# Roadmap

Akari Tool — Windows System Optimization GUI

---

## Milestone: v1.0 — Feature Enhancements & Quality Improvements

**Goal**: Build user-requested enhancements and polish the existing UX through end-to-end MVP phases, each delivering observable user behaviors and validating improvements before moving on.

### Mode Notes
- **Phase 3 onward**: Switch to `standard` mode once undo system is delivered (non-linear regression not yet feasible in v1)

| # | Phase | Goal | Requirements | Success Criteria | ETA |
|---|-------|------|--------------|------------------|------|
| 1 | Batch Restore Point Creation — Single button to create restore point before running changes in any tab | REQ-UX-03, HOME-XX | 1. User clicks "Create Pre-flight Backup" button <br>2. App creates system restore point via `SystemRestore/CreateVr` WMI call or `wmic` fallback <br>3. Confirmation shows restore point name/time <br>4. Error handled if already at max restore points (limit 6+1) | [ ] [ ] [ ] | TBD |
| 2 | Visual Change Log System — Show diff after running sections with export option | REQ-UX-04, HOME-XX | 1. User runs one or more tabs <br>2. App displays before/after change summary per registry key/service modified in collapsible panel <br>3. User can export to text/HTML for sharing/review (optional) <br>4. Change log persist to user config directory (<code>%APPDATA%/AkariTool/ChangeLogs</code>) | [ ] [ ] [ ] | TBD |
| 3 | Undo/Rollback System — Revert last N changes safely without reboot | REQ-UX-05, WINDOWS-XX, ADVANCED-XX | 1. User initiates "Rollback Last Changes" from Home or undo panel <br>2. App validates required admin rights and warns about dependencies (e.g., re-enabling Defender after disabling it) <br>3. System rolls back registry/service changes per recorded history up to last N toggles <br>4. User sees rollback summary with confirmation prompt <br>5. Undo log persists in user config directory | [ ] [ ] [ ] | TBD |
| 4 | Pre-flight Validation — Check hardware/specs before applying certain tweaks | UX-XX, CHECK-XX, GRAPHICS-XX | 1. App validates prerequisites for DDU (e.g., NVIDIA/AMD driver installed, GPU type) <br>2. Shows "Cannot proceed without X" with guidance link when check fails <br>3. Validation runs only once per tab entry or before heavy operations <br>4. Optional: Skip validation in advanced users' config for speed | [ ] [ ] [ ] | TBD |
| 5 | User Education Tour — Guided new-user walkthrough with tooltips | UX-01, HOMEE-XX | 1. First-run user sees optional "Quick Tour" checkbox during startup or via settings toggle <br>2. Tooltips explain each section's purpose with safety warnings for Advanced tab items <br>3. User can progress at own pace, pause tour at any point <br>4. Tour records completion in config and skips on subsequent runs unless reset | [ ] [ ] [ ] | TBD |
| 6 | Individual Tweaks Category Reorganization — Group tweaks by function (network, power, privacy) instead of strict registry path order | TWEAKS-01 ~ TWEAKS-75+ | 1. Tweaks sorted into collapsible groups: Networking, Power, Privacy, Display, Gaming <br>2. Collapsed by default; user expands relevant category <br>3. Star button marks user's recommended option for each toggle (from FR33THY Ultimate) still in place <br>4. No UI breaks for existing users (grouping only affects new app sessions if config persists) | [ ] [ ] [ ] | TBD |

---

## Coverage Table

| Requirement | Phase |
|-------------|-------|
| UX-01 — Single-file distribution | Phase 1 (implied current state, validated in PROJECT.md) |
| UX-02 — Batch optimization workflow | All phases (implied) |
| UX-03 — Pre-flight restore point | Phase 1 |
| UX-04 — Visual change logs | Phase 2 |
| UX-05 — Undo/rollback system | Phase 3 |
| HOME-01 ~ HOME-04 | All phases (Home tab is current) |
| CHECK-01 ~ CHECK-03 | Phase 4 |
| REFRESH-01 ~ REFRESH-04 | All phases (Refresh handlers current) |
| SETUP-01 ~ SETUP-06 | All phases (Setup handlers current) |
| INSTALLERS-01 ~ INSTALLERS-03 | Phase 4, 5 |
| GRAPHICS-01 ~ GRAPHICS-03 | Phase 4 |
| WINDOWS-01 ~ WINDOWS-04 | Phase 4, 6 |
| HARDWARE-01 ~ HARDWARE-03 | All phases (Hardware handlers current) |
| TWEAKS-01 ~ TWEAKS-75+ | Phase 6 |

---

## Current State

All phases except #1–#6 are **Not Started**. Milestone v1.0 begins with implementation of these six enhancements. After completion, the project enters **Milestone v1.1** focusing on long-term stability refinements and edge-case handling.

---

*Auto-generated: Oct 04, 2026*
