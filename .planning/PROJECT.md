# Akari Tool

## What This Is

A clean Windows 10/11-styled WPF GUI (Mica backdrop, dark theme) that wraps FR33THY's **Ultimate** Windows system tweaking scripts. Point-and-click access to dozens of optimizations, debloat steps, installers, and diagnostics — no console menus, no typing numbers, just one intuitive interface.

The app ships as a single self-contained file (`akari.ps1`) compiled from source files. It has no external dependencies, embeds all assets (GUI, styles, logos), and offers batch distribution for users of all technical levels.

**Current state**: A mature PowerShell-WPF hybrid that delegates some menu-driven tweaks to Ultimate's original console scripts while handling registry toggles and app installs inline as native one-click actions.

## Core Value

Give any Windows user safe, easy access to deep system optimizations without needing command-line knowledge.

## Requirements

### Validated

<!-- Shipped and confirmed valuable. Derived from existing codebase. -->

- [✓] **Home tab** — Welcome + safety notice, live "This PC" info, recommended-path shortcuts to all sections, Desktop shortcut (online/offline), credits
- [✓] **Check tab** — BIOS settings & updates, PC stability check (OCCT), hardware diagnostics
- [✓] **Refresh tab** — Factory reset options, Win10/11 reinstall with autounattend, local account creation, update driver block/unblock, network driver → BIOS
- [✓] **Setup tab** — BitLocker management, memory compression, background apps, keys/activation, Pro conversion, date/language/region, startup apps, Edge/Store settings, pause updates
- [✓] **Installers tab** — winget installs for launchers, browsers & apps (each pre-debloated), GPU tools
- [✓] **Graphics tab** — DDU driver clean/install/debloat (NVIDIA/AMD/Intel), GPU settings, HDCP, P0, MSI mode, DirectX/C++, resolution, HAGS
- [✓] **Windows tab** — Taskbar/Start layout & shortcuts, context menu, black theme, bloatware removal/checks + native reinstall (Store, UWP, OneDrive, Snipping, RDC, winget), Widgets/Copilot/Game Bar/Edge settings, Control Panel/Notepad/Sound tweaks, performance tuning (power plan, write cache, device/network power, IPv4), Game Mode/Pointer/Scaling, UAC, Defender Optimize, Autoruns/Cleanup/Restore Point/Core Isolation
- [✓] **Hardware tab** — Higher scaling (no accel), monitor optimization, background polling cap, mouse/controller polling tests, controller overclock, bufferbloat test, PC build guide
- [✓] **Advanced tab** — Defender disable, firewall, Spectre/Meltdown mitigations, DEP, download warning, services, MMAgent, NVMe driver, shell/mobsync, MPO/flip/ULPS/ReBar, keyboard shortcuts, SMT/Core 1 Thread 1/Priority, WHQL bypass
- [✓] **Individual Tweaks tab** — SSVCHOST Split Threshold, Win32 Priority Separation scheduling, plus 169 granular Control Panel tweaks grouped and collapsible, Optimize/Default per row
- [✓] **Inline handlers** — Simple registry toggles and per-app installers implemented as native one-click actions in each tab's handler
- [✓] **Embedded console delegates** — Interactive, menu-driven tweaks (SMT/HT, Core 1 Thread 1, Priority, Bloatware) run via `Invoke-ConsoleScript`, embedded at compile time, self-contained within app

### Active

<!-- Current scope. Building toward these. -->

- [ ] **Batch Restore Point Creation** — Single button in Home tab to create restore point before applying any changes across all tabs
- [ ] **Visual Change Logs** — After running sections, show a diff of what changed with optional export to text/HTML for sharing
- [ ] **Undo/Rollback System** — Track last N changes per category and provide safe rollback without reboot
- [ ] **Pre-flight Validation** — Check hardware specs before certain tweaks (e.g., OCCT tests, GPU VRAM for MSI mode)
- [ ] **User Education Tour** — Guided new-user walkthrough with tooltips explaining each section's purpose and recommended toggles

### Out of Scope

<!-- Explicit boundaries. Includes reasoning to prevent re-adding. -->

- Real-time toggle persistence across app restarts without registry sync (not currently in Ultimate, would require major refactor)
- Cloud-based configuration profiles/user-sync features (outside scope of standalone app distribution)
- Mobile platform support (WPF is Windows-only)

## Context

<!-- Background information that informs implementation. -->

**Technology:**
- **OS**: Windows 10/11 (Home/Pro/LTSC/IoT/Server)
- **Stack**: PowerShell (7+ for compilation, runtime uses embedded scripts), WPF + DWM for UI
- **Distribution**: Single-file standalone — no external dependencies, assets embedded as base64
- **Architecture**: Modular XAML panels injected into main window shell at compile time

**Code Structure:**
```
akari.ps1              ← COMPILED output from sources (800+ lines of embedded content)
Compile.ps1           ← Builds akari.ps1 by concatenating components in fixed order
  ├─ scripts/         ← Shared startup and main logic
  ├─ functions/       ← Tab handlers (inline for simple toggles, console delegates for complex)
  └─ xaml/            ← MainWindow shell + panel fragments per tab
assets/               ← Logo, icons embedded at compile time
```

**Distribution Model:**
- Users run `akari.ps1` via elevated terminal (app self-elevates on launch)
- No installer needed — drops as single executable to Desktop
- Embedded scripts mean no external folders to misplace or update separately

**Compatibility Considerations:**
- Some tweaks require specific Windows versions (e.g., memory compression is W11+)
- Advanced tab changes may affect system security/stability
- App requires admin rights for registry/system-level changes

## Constraints

- **OS Compatibility**: Win10/Win11 only (WPF limitation)
- **Admin Rights Required**: Necessary for registry, service, driver modifications
- **Internet Access**: Many installers and content fetch remotely; some embedded scripts need network access
- **Single-File Distribution**: All assets must be baked in at compile time; can't have separate update mechanism
- **Windows Tweaks Only**: App is Windows-specific optimization tool

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| **Single-file distribution** | Ease of deployment for non-tech users | ✓ Good — one file, no installer needed |
| **Inline vs delegate tradeoff** | Keep app lean by embedding simple handlers, delegate complex/interactive ones to Ultimate's console scripts | ✓ Good — clean separation of concerns |
| **Mica + dark theme UI** | Modern Windows native look and feel | ✓ Good — consistent with OS design language |
| **Compile-time asset baking** | Fully offline capable once distributed | ✓ Good — no external folder dependencies |

---

*Last updated: Oct 04, 2026 after initialization*

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active

**After each milestone** (via `/gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state
