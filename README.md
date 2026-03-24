<!-- markdownlint-disable MD033 -->

# afterflash

<p align="center">
  <img src="assets/afterflash.png" alt="afterflash logo" width="500">
</p>

Windows PowerShell setup script for quickly applying post-build system tweaks,
performance settings, and optional debloat actions on a fresh PC. Built out of
my personal interest in PC building and optimization, with the goal of saving
time and reducing repetitive setup work after each build.

<br>

## Features

---

### Setup Modes

- **Interactive** — each step is shown with a confirmation prompt
- **Quick Setup** — applies all tweaks automatically without prompting (websites skipped)
- **System Restore Point** — optionally created before any changes are made
- **Changes Report** — summary of all applied changes printed at the end

<br>

### System Information

- Overview of CPU, GPU, RAM, mainboard, BIOS version and OS

<br>

### Driver Downloads

- GPU driver page for AMD or NVIDIA (auto-detected)
- Chipset driver page for Intel or AMD (auto-detected)
- DDU (Display Driver Uninstaller) download page

<br>

### Performance *(applied with confirmation)*

- Hardware-Accelerated GPU Scheduling: **On**
- Variable Refresh Rate: **On**
- Game Mode: **Off**
- Xbox Game Bar: **Off**
- Fullscreen Optimizations: **Off** (globally)
- High-Precision Timer Resolution: **On** (`useplatformtick` + `disabledynamictick`)
- MSI Mode for GPU: **On** (sets `MSISupported=1` + `DevicePriority=3`)
- Mouse Acceleration: **Off**
- Power Plan: **Ultimate Performance** / **High Performance** / **Balanced** for X3D CPUs (auto-detected)

<br>

### Privacy *(applied with confirmation)*

- Optional diagnostic data: **disabled**
- Delivery Optimization P2P: **disabled**

<br>

### Network *(applied with confirmation)*

- DNS servers: **Cloudflare** (1.1.1.1 / 1.0.0.1) or **Google** (8.8.8.8 / 8.8.4.4) — applied to all active adapters
- NIC power saving: **disabled**

<br>

### UI *(applied with confirmation)*

- Dark Mode: **On**
- File extensions in Explorer: **visible**
- Hidden files in Explorer: **visible**

<br>

### Optional

- System Protection (restore points) on C:
- Clipboard History
- Do Not Disturb / Notifications

<br>

### Tools

- [Ninite](https://ninite.com/) for bulk app installation
- [HWiNFO64](https://www.hwinfo.com/download/) for hardware monitoring
- [GPU-Z](https://www.techpowerup.com/gpuz/) for GPU information
- [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html) for CPU information
- [CrystalDiskMark](https://crystalmark.info/en/software/crystaldiskmark/) for storage benchmarking
- Windows Update trigger
- [Win11Debloat](https://github.com/Raphire/Win11Debloat) integration

<br>

## Quick Start

---

### Option A — Standalone EXE *(recommended for USB use)*

Download `afterflash.exe` and run it directly — no installation needed.

<br>

### Option B — PowerShell Script

1. **Clone or download** this repository
2. **Run** the setup script (will prompt for elevation automatically):

```powershell
.\scripts\setup.ps1
```

<br>

### Option C — Standalone BAT

Run `afterflash-standalone.bat` directly. All PowerShell code is embedded —
no additional files required.

<br>

### If PowerShell says the script is not digitally signed

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
Get-ChildItem -Path . -Filter *.ps1 -Recurse | Unblock-File
```

<br>

## Requirements

---

- **Windows 10** or **Windows 11**
- **PowerShell 5.0+** (pre-installed on Windows 10/11)
- **Administrator privileges** (script will request elevation automatically)

<br>

## Verification

---

After running the setup, use the verification script to manually check
that settings were applied correctly:

```powershell
.\scripts\verify.ps1
```

This script opens relevant Windows settings pages without making any changes.

<br>

## Building the EXE

---

The EXE is built from `afterflash-standalone.bat` using the build script:

```powershell
.\tools\build-exe.ps1
```

Requires PS2EXE (installed automatically if missing) and PowerShell with
administrator privileges.

<br>

## Development

---

### Running Tests

#### Pester Unit Tests

```powershell
Remove-Module Pester -Force -ErrorAction SilentlyContinue
Invoke-Pester -Path ./tests -Output Detailed
```

#### PSScriptAnalyzer

```powershell
Invoke-ScriptAnalyzer -Path ./scripts -Recurse -Settings ./scripts/PSScriptAnalyzerSettings.psd1
```

#### Markdown Linting

```powershell
npm install -g markdownlint-cli
markdownlint -c .markdownlint.json .
```

<br>

## External Tools

---

### Win11Debloat

[Win11Debloat](https://github.com/Raphire/Win11Debloat) by Raphire is not bundled.
If selected, the script launches it via its official quick-launch command:

```powershell
& ([scriptblock]::Create((irm "https://debloat.raphi.re/")))
```

<br>

### Ninite

[Ninite](https://ninite.com/) is not bundled. If selected, the script opens
the official website in the browser.

<br>

## License

---

This project is licensed under the [MIT License](LICENSE).
