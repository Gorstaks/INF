# INF

Security templates in INF format for the Windows Security Configuration Editor (SCE), plus an `Autorun.inf` for install media.

> **Warning:** these templates change account, audit, registry and user-rights settings machine-wide. They can lock you out or break applications. Test in a virtual machine and take a restore point first.

## Files

| File | Description |
| --- | --- |
| `GSecurity.inf` | GSecurity security template. Sections: `System Access` (password and lockout policy, built-in account state), `Event Audit`, `Registry Values` (UAC prompt behavior, logon, Winlogon and recovery console settings) and `Privilege Rights`. |
| `HISECWS.INF` | Microsoft's High Security Workstation template (HighWS, version 05.10.HW.0000), included as a reference baseline. |
| `NTX_SAFER.INF` | Configures Software Restriction Policies (SAFER) on Windows 8 and Server 2012 up to Windows 11 and Server 2025. Its header explains that SECPOL.MSC and GPEDIT.MSC read additional SAFER rules only from `%SystemRoot%\System32\GroupPolicy\Machine\REGISTRY.POL`, not from the registry. |
| `Autorun.inf` | Launches `sources\setup.exe` when the disc or drive is opened. Intended for Windows install media, not for security hardening. |

## Usage

Apply a template from an elevated Command Prompt with `secedit`:

```bat
secedit /configure /db %windir%\security\database\gsecurity.sdb /cfg GSecurity.inf /areas SECURITYPOLICY
```

Or open **Security Configuration and Analysis** (`mmc`, add the snap-in), create a database, import the template and choose **Configure Computer Now**.

To see what a template would change before applying it, use **Analyze Computer Now** in the same snap-in.

## Notes

- `GSecurity.inf` sets `LockoutBadCount = 10` and leaves the built-in Administrator and Guest accounts disabled.
- `NTX_SAFER.INF` and `HISECWS.INF` carry their original author headers and licensing notes. Keep them intact.
- The same settings are available as a Group Policy backup in the `Policies` project and as a provisioning package in `Provisioning`.

## Author

Gorstak
