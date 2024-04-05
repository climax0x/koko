# CustomShellHost.exe Execute

CustomShellHost.exe is a host process specifically designed for environments where Windows is configured to run in Kiosk mode, using custom shells instead of the standard Windows shell interface. This capability is crucial for setting up single-purpose devices, like information kiosks or retail terminals, providing a streamlined and controlled user experience. However, just as with any powerful tool, it can be exploited for malicious purposes.

## What is CustomShellHost.exe?

`CustomShellHost.exe` serves as a backbone for custom shell applications, enabling a wide range of specialized user interfaces to replace the standard Windows shell. In Kiosk mode, it ensures that the device runs a specific application or environment, limiting access to other parts of the Windows operating system to prevent misuse or tampering.

### Paths

- `C:\Windows\System32\CustomShellHost.exe`

### Resources

- [Twitter Thread by John Carroll (@YoSignals)](https://twitter.com/YoSignals/status/1381353520088113154) discussing CustomShellHost.exe uses.
- [Microsoft Docs on Shell Launcher](https://docs.microsoft.com/en-us/windows/configuration/kiosk-shelllauncher) for configuring custom shells in Windows.

### Acknowledgements

- John Carroll (@YoSignals) for his insights and contributions to the understanding of CustomShellHost.exe in security contexts.

### Detection

CustomShellHost.exe typically runs only on specialized devices configured for single-purpose use. Its execution in a general-purpose workstation environment may indicate an attempt to misuse system resources.

- IOC: The presence and execution of CustomShellHost.exe on non-kiosk mode workstations.
- Sigma Rule: [proc_creation_win_lolbin_customshellhost.yml](https://github.com/SigmaHQ/sigma/blob/main/rules/windows/process_creation/win_lolbin_customshellhost.yml) helps in detecting suspicious instances of CustomShellHost.exe being used.

## Execution Example

The following demonstrates how `CustomShellHost.exe` can be misused to execute `explorer.exe`, potentially circumventing security measures designed to restrict user access on a kiosk or similarly restricted device.

### Command:

```cmd
CustomShellHost.exe /explorer.exe /NoShellRegistrationCheck
