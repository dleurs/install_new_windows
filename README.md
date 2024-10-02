```
notepad $PROFILE
```

```
function Get-GitBranch {
    if (Test-Path .git) {
        $branch = git rev-parse --abbrev-ref HEAD
        " [$branch]"
    }
}

function prompt {
    $p = Split-Path -leaf -path (Get-Location)
    Write-Host "$p" -NoNewline
    Write-Host (Get-GitBranch) -NoNewline -ForegroundColor Yellow
    Write-Host "> " -NoNewline
    return " "
}

function gof {
    Set-Location 'C:\Users\dleurs\Documents\Flutter'
}
```
Open Powershell in admin, then copy/paste and select 1 and restart windows
```
$mode = Read-host "How do you like your mouse scroll (0 or 1)?"; Get-PnpDevice -Class Mouse -PresentOnly -Status OK | ForEach-Object { "$($_.Name): $($_.DeviceID)"; Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters" -Name FlipFlopWheel -Value $mode; "+--- Value of FlipFlopWheel is set to " + (Get-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters").FlipFlopWheel + "`n" }
```
