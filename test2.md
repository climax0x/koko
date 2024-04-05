# Forfiles Execute Alternate Data Streams

**Description:**  
Selects and executes a command on a file or set of files. This command is useful for batch processing.

**Paths:**  
- `C:\Windows\System32\forfiles.exe`  
- `C:\Windows\SysWOW64\forfiles.exe`  

**Resources:**  
- [Twitter - @vector_sec](https://twitter.com/vector_sec/status/896049052642533376)
- [GitHub Gist - @api0cradle](https://gist.github.com/api0cradle/cdd2d0d0ec9abb686f0e89306e277b8f)
- [Oddvar Moe's Blog](https://oddvar.moe/2018/01/14/putting-data-in-alternate-data-streams-and-how-to-execute-it/)

**Acknowledgements:**  
- Eric (@vector_sec)
- Oddvar Moe (@oddvarmoe)

**Detection:**  
- Sigma: [proc_creation_win_lolbin_forfiles.yml](https://github.com/SigmaHQ/sigma/blob/main/rules/windows/process_creation/win_lolbin_forfiles.yml)

**Execute:**

- **Description:**  
  Executes calc.exe since there is a match for notepad.exe in the c:\windows\System32 folder.
- **Command:**  
  `<Command to be filled in>`
