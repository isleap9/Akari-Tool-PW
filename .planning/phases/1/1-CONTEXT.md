# 1-CONTEXT.md

Phase 1: Batch Restore Point Creation — Implementation Decisions

---

## Domain

Deliver a single-button restore point creation feature in the Home tab that users can invoke before applying any system tweaks across all tabs. The button creates a Windows system restore point via `SystemRestore/CreateVr` WMI call or `wmic` fallback, with status bar confirmation and error handling.

---

## Canonical refs

- `.planning/PROJECT.md` — Project context, validated requirements, current state
- `.planning/REQUIREMENTS.md` — REQ-UX-03 (restore point creation) definition + DoD guidelines
- `.planning/ROADMAP.md` — Phase 1 goal, success criteria table, MVP mode constraints

---

## Code Context

### App Architecture

Akari Tool is a single-file compiled WPF app with inline handlers for simple registry toggles and console delegates for complex interactive tweaks. Restore point creation will be an **inline handler** pattern that:
- Uses `SystemManagementPack` WMI class as primary method
- Falls back to `wmic` for older Windows scenarios
- Logs to status bar via `$status` parameter for inline progress updates

### Home Tab Layout

The button will reuse the existing [`xaml/panels/00-Home.xaml`](../xaml/panels/00-Home.xaml) layout, placed in an "Actions" panel similar to credits and links. This avoids adding a floating action button (visual clutter) or context menu implementation (scope creep).

---

## Decisions

### UI Location ✅

**Decision**: Home tab "Actions" panel

**Rationale**: 
- Reuses existing Home layout patterns
- Logical placement matching user mental model ("backup before changes")
- No new UI components needed (consistent with MVP simplicity)
- Avoids floating action button confusion and context menu complexity

---

### Restore Point Naming Convention ✅

**Decision**: `[Akari Tool] {Timestamp}` as default format `YYYY-MM-DD_HH-mm-ss`

**Rationale**:
- Clearly identifies source (akari tool) vs manual restore points
- Timestamp enables easy recognition in Windows UI sorting by creation time
- Machine-readable date for automation tools/scripts
- Optional user override can be added later without changing MVP

**Example output**: `[Akari Tool] 2026-10-04_15-30-00`

---

### Post-Creation Feedback ✅

**Decision**: Status bar message only (no modal dialog) for MVP

**Rationale**:
- Non-intrusive to workflow; matches existing inline handler patterns
- Status bar appears for ~5 seconds then disappears automatically
- Redundant safety acceptable if user misses it — they can verify in System Restore settings
- Modal dialog deferred to Phase 2 with optional toggle if UX audit finds insufficient

**Implementation**: Use `$status = "Restore point created successfully"` parameter in handler, leveraged by WPF status bar control or equivalent.

---

### Naming Format ✅

**Decision**: `[Akari Tool] {Timestamp}` as default format `YYYY-MM-DD_HH-mm-ss`

**Rationale**:
- Clearly identifies source vs manual restore points
- Timestamp enables easy recognition in Windows UI sorting by creation time
- Machine-readable date for automation tools/scripts
- Optional user override can be added later without changing MVP

---

### Pre-flight Warnings ✅

**Decision**: Always prompt before creation (safe default, no silent mode yet)

**Rationale**:
- Safety-first; matches restore point best practices and Microsoft recommendations
- User explicitly confirms safety action (good habit reinforcement)
- No toggle needed now — advanced users can edit config if they want speed
- Silent auto-create mode deferred to Phase 2 or via `workflow.silentRestorePointCreation` config option later

---

## Deferred Ideas

None for MVP. The following could be added in future phases:
- Optional modal dialog toggle
- User-chosen restore point name override
- Auto-create restore points at tab entry (if changes detected)
- Context menu right-click restore point action

---

*Captured: Oct 04, 2026*
