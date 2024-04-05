# Forfiles.exe Execution and Alternate Data Streams

`Forfiles.exe` is a versatile command-line utility available in Windows that allows for the selection and execution of commands on a set of files. This functionality is particularly useful for batch processing. One of its less conventional uses involves the execution of commands or binaries hidden within alternate data streams (ADS), allowing for potential evasion of security measures.

## Paths

- `C:\Windows\System32\forfiles.exe`
- `C:\Windows\SysWOW64\forfiles.exe`

## Resources

- [Vector_Sec on Twitter](https://twitter.com/vector_sec/status/896049052642533376) discusses forfiles usage scenarios.
- [API0CRADLE's Gist on GitHub](https://gist.github.com/api0cradle/cdd2d0d0ec9abb686f0e89306e277b8f) provides examples of forfiles in action.
- [Oddvar Moe's Blog](https://oddvar.moe/2018/01/14/putting-data-in-alternate-data-streams-and-how-to-execute-it/) delves into the concept of alternate data streams and their execution.

## Acknowledgements

- Eric (@vector_sec) for highlighting forfiles' potential in security contexts.
- Oddvar Moe (@oddvarmoe) for detailed research on ADS and forfiles.

## Detection

Detection strategies focus on monitoring unusual forfiles.exe activity, as its misuse can signify an attempt to execute hidden or malicious commands.

- Sigma Rule: [proc_creation_win_lolbin_forfiles.yml](https://github.com/SigmaHQ/sigma/blob/main/rules/windows/process_creation/win_lolbin_forfiles.yml) aids in detecting suspicious forfiles.exe usage.

## Execution

### Using forfiles to Execute Commands

#### Scenario: Executing calc.exe

```cmd
forfiles /p c:\windows\system32 /m notepad.exe /c calc.exe



Use case: Employ forfiles to initiate a new process, potentially circumventing security detections.

Privileges required: User

Operating systems: Windows Vista through Windows 11

ATT&CK® technique: T1202 - Indirect Command Execution

Alternate Data Streams (ADS)
Scenario: Launching an Executable from ADS

forfiles /p c:\windows\system32 /m notepad.exe /c "c:\folder\normal.dll:evil.exe"


Use case: Utilizes forfiles to initiate a new process from a binary concealed within an alternate data stream, offering a method to hide malicious activity.

Privileges required: User

Operating systems: Windows Vista through Windows 11
