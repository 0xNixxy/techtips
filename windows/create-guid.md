# Create GUID via PowerShell

PowerShell 5.1 comes pre-packaged with a nifty cmdlet to generate new Globally
Unique Identifier (GUIDs) for you.

> [!NOTE]
> PowerShell 5.1 comes pre-packaged in Windows 11.

## Generate a new GUID

You can generate a new GUID in PowerShell using

```powershell
[guid]::NewGuid()
```

## Generate GUID in Registry format

Alternatively, you can also generate a new GUID in Registry format using

```powershell
'{'+[guid]::NewGuid().ToString()+'}'
```
