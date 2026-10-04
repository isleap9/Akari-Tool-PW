# Copilot Instructions — Akari Tool

When generating code or reviewing commits for this project:

## Architecture Summary

Akari Tool is a **single-file Windows GUI** that wraps FR33THY's Ultimate system tweak scripts. It compiles modular components into `akari.ps1` at build time via `Compile.ps1`.

### Runtime Structure (Post-Compilation)

```
akari.ps1               ← Embedded content, no external deps
├─ Scripts embedded from:
  ├─ scripts/start.ps1  ← Admin elevation + WPF/DWM init
  ├─ scripts/main.ps1   ← XAML parsing, button wiring, window show
  ├─ functions/public/*  ← Tab handlers (Invoke-*Action)
  ├─ functions/private/* ← Helpers (Invoke-RunInBackground, Invoke-ConsoleScript)
  ├─ xaml/MainWindow.xaml   ← Shell with @PANELS@ marker
  └─ xaml/panels/*       ← Panel fragments injected at compile time
└─ assets/base64/*      ← Logos/icons embedded at compile time
```

### Compile-Time Injection Flow

```powershell
Compile.ps1 reads:
  ├─ All public/*.ps1 function files (sorted by NN- prefix)
  ├─ config/*.json for embedded $sync.configs variables
  └─ xaml/panels/*.xaml into MainWindow.xaml's @PANELS@ marker
  
Outputs: akari.ps1 (one single-file executable)
```

### Two Handler Types

- **Inline Handlers** — Simple registry toggles, app installs run as native one-click actions in handler script. These can be edited directly.

  Example pattern:
  ```powershell
 function Invoke-BtnFirewallDisable {
    Set-ItemProperty -Path HKLM\SOFTWARE\Policies\Microsof... -Value "Disabled"
  }
  ```

- **Console Delegates** — Complex interactive tweaks (SMT/HT, Core 1 Thread 1) run via `Invoke-ConsoleScript`, which decodes embedded asset from `Assets/Text/<tweakname>.ps1` bakes in at compile time and launches it in elevated console. User picks option there.

  Handler example:
  ```powershell
  function Invoke-BtnPrioritySeparation {
      Invoke-ConsoleScript -Asset "SSVCHOST-Split-Threshold.ps1"
  }
  
  # During compile, Assets/Text is baked into akari.ps1's embedded code as base64 string.
  ```

## GSD Workflow Integration

We use **GSD methodology** for feature development:

```bash
/gsd-discuss-phase <phase-number>     # Gather context before planning
/gsd-plan-phase <phase-number>        # Create detailed plan with DoD, test cases
/gsd-execute-phase <phase-number>      # Build incrementally with verification
/gsd-ui-review <phase-number>          # UI audit for new XAML panels
```

All planning artifacts live in `.planning/` and are tracked in git. They serve as living documentation alongside implementation code.

## Git Behavior

- **Tracked**: `.git`, `config.json`, `PROJECT.md`, `REQUIREMENTS.md`, `ROADMAP.md`, `.planning/*`
- **Ignored**: `akari.ps1` (compiled binary), `*.ps1.psx`
- **Local-only option**: Uncomment `.planning/` in `.gitignore` and set `commit_docs: false`

## Code Style Preferences

### Function Templates

```powershell
function Invoke-*Action {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$false)] [string] -Description $d = ''
    )

    # Validate admin if needed
    if (-not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)) {
        Write-Warning "Requires administrator privileges"
        return
    }

    try {
        # Inline logic or console delegate invocation
        Invoke-*SubAction  # Replace with actual action code

        return "Success: Action completed via $Description"
    }
    catch {
        Write-Error "$($_.Exception.Message)" -ErrorAction Continue
        return "Failed: $_"
    }
}
```

### Console Delegate Pattern

```powershell
function Invoke-*ComplexTweak {
    # Call console delegate
    $scriptPath = "Assets/Text/<tweaks>/<tweaks_tweaks_tweaks_75+>.ps1"
    
    if (-not (Test-Path "$scriptPath")) {
        Write-Warning "Embedded tweak script not found: $scriptPath"
        return
    }

    # Decode from base64 embedded asset and launch in elevated console
    Invoke-ConsoleScript -Asset "$scriptPath" -Description $d
}
```

### XAML Panel Fragments

Each panel should use `<!-- @PANELS@ -->` convention for auto-wiring:

```xml
<UserControl Name="NN-Tweaks" ...>
    <!-- Button names auto-wire to Invoke-* handlers by convention -->
    <Button Name="BtnRestorePointCreate" Content="⭐ Create Backup" />
    <StackPanel ...>
        <Expander Header="Network">
            <CheckBox IsChecked="$config.Network.Tweaks.V1..." />
        </Expander>
    </StackPanel>
    
    <!-- @PANELS@ marker is injected by Compile.ps1 -->
</UserControl>
```

## Testing Checklist (Before Commit)

Before committing any feature:

- [ ] Tested in Windows 10 and 11 where applicable
- [ ] Admin rights handled correctly
- [ ] Error messages are user-friendly, not just raw exceptions  
- [ ] Progress via status bar (`$status` parameter if used) works
- [ ] No console errors after execution (especially for embedded delegates)
- [ ] Toggle persists or appropriately resets per handler design
- [ ] If new XAML added, panel is injected correctly by `Compile.ps1`

## Project Context

**What**: Batch Windows system optimization GUI with 9 tabs worth of features
**Core value**: Safe, easy access to deep system tweaks without CLI knowledge  
**Distribution**: Single-file standalone via elevated terminal launch  
**Tweaks count**: ~180+ granular toggles + menu-driven interactive ones  
**Upstream**: FR33THY's Ultimate (not affiliated but wraps it)
