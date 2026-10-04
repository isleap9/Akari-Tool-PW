# Requirements

## Overview

This document defines the features and capabilities of Akari Tool. Requirements are grouped by feature category with REQ-IDs for traceability in ROADMAP.md and acceptance criteria verification.

**Version 1.0** captures current validated capabilities plus enhancements to build next.

---

## v1 Requirements (Active)

### User Experience (UX) & Distribution

| ID | Requirement | Priority |
|-----|-------------|----------|
| **UX-01**: Users can run `akari.ps1` as single file without installer or external dependencies | P0 |
| **UX-02**: Users complete batch system optimization across all tabs in under 30 minutes via point-and-click flow | P0 |
| **UX-03**: Users create restore point before running any changes with single button click | P1 |
| **UX-04**: Users see visual summary/diff of changes after completing sections | P1 |
| **UX-05**: Users safely revert last N changes without reboot via undo system | P1 |

### Home Tab (Landing & Information)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **HOME-01**: Users see welcome screen with safety notice and recommended-path shortcuts to all sections | P0 |
| **HOME-02**: Users check current "This PC" specs live without leaving app | P0 |
| **HOME-03**: Users create Desktop shortcut (online/offline install options) with single click | P0 |
| **HOME-04**: Users review credits and attribution to FR33THY/Ultimate | P0 |

### Check Tab (Diagnostics & BIOS)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **CHECK-01**: Users run BIOS update check with guided settings walkthrough | P0 |
| **CHECK-02**: Users run PC stability check via OCCT stress test | P0 |
| **CHECK-03**: Users view diagnostic report of hardware health post-check | P0 |

### Refresh Tab (Reset & Recovery)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **REFRESH-01**: Users perform factory reset with guided options via autounattend workflow | P0 |
| **REFRESH-02**: Users reinstall Windows 10/11 locally in automated fashion | P0 |
| **REFRESH-03**: Users create local account without Microsoft login during setup | P0 |
| **REFRESH-04**: Users block or unblock update drivers (including graphics) with single toggle | P1 |

### Setup Tab (System Configuration)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **SETUP-01**: Users manage BitLocker encryption status and keys through app | P0 |
| **SETUP-02**: Users enable memory compression to save SSD write cycles | P0 |
| **SETUP-03**: Users manage background apps per category (battery life control) | P0 |
| **SETUP-04**: Users convert Home edition to Pro with online activation link | P0 |
| **SETUP-05**: Users customize date, language, and regional settings in app | P1 |
| **SETUP-06**: Users pause Windows updates temporarily without breaking installers | P1 |

### Installers Tab (App Storefront)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **INSTALLERS-01**: Users install popular apps (launchers, browsers, utilities) with pre-debloat options | P0 |
| **INSTALLERS-02**: Users install GPU tools (MSI Afterburner, etc.) from curated list | P0 |
| **INSTALLERS-03**: Users search winget catalog filtered to vetted apps only | P1 |

### Graphics Tab (GPU Configuration)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **GRAPHICS-01**: Users clean GPU drivers via DDU integration with guided workflow | P0 |
| **GRAPHICS-02**: Users install/debloat NVIDIA, AMD, or Intel drivers from app menus | P0 |
| **GRAPHICS-03**: Users enable HDCP, P0, MSI mode for gaming optimization | P1 |

### Windows Tab (UI & Bloat Removal)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **WINDOWS-01**: Users customize taskbar/Start layout with pinned apps and shortcuts | P0 |
| **WINDOWS-02**: Users bloatware removal via native uninstallers + Store app deletion | P0 |
| **WINDOWS-03**: Users toggle Widgets/Copilot/Game Bar/Edge settings per preference | P1 |
| **WINDOWS-04**: Users optimize performance (power plan, write cache, network power) | P0 |

### Hardware Tab (Peripherals Tuning)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **HARDWARE-01**: Users adjust monitor scaling without acceleration artifacts | P0 |
| **HARDWARE-02**: Users test mouse/controller polling rates for optimization | P0 |
| **HARDWARE-03**: Users view bufferbloat test results and settings guide | P1 |

### Advanced Tab (Use-with-Care)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **ADVANCED-01**: Users disable Defender selectively (with warnings and restore-point advice) | ⚠️ Security Review |
| **ADVANCED-02**: Users toggle firewall rules per app/zone | P1 |
| **ADVANCED-03**: Users disable Spectre/Meltdown mitigations with informed consent UI | ⚠️ Security Review |

### Individual Tweaks Tab (Registry & Performance)

| ID | Requirement | Priority |
|-----|-------------|----------|
| **TWEAKS-01**: Users schedule SSVCHOST Split Threshold per-core optimizations | P0 |
| **TWEAKS-02**: Users enable Win32 Priority Separation for gaming performance | P0 |
| **TWEAKS-03**: Users access 169 granular Control Panel tweaks grouped by category with optimize/default toggles | P0 |

---

## v2 Requirements (Future, Out of Scope for v1)

### Network Efficiency & Sync

| ID | Requirement | Priority |
|-----|-------------|----------|
| **SYNCHRO-01**: Users sync config profiles between devices via cloud profile store | Low priority |
| **SYNCHRO-02**: Users share custom tweak sets with other users as exportable JSON configs | Deferring |

---

## Definition of Done (DoD)

All v1 requirements must achieve:

1. **Functionality** — Feature works reliably across Windows 10 and 11 where applicable
2. **Error Handling** — App recovers gracefully and displays user-friendly messages on failure
3. **Admin Handling** — App self-elevates or clearly communicates need for admin rights
4. **Persistence** — Changes persist after app restart (unless design specifies otherwise)
5. **No Side Effects** — Unrelated registry services, and drivers remain unaffected unless toggled

---

*Auto-generated from project documentation analysis*
