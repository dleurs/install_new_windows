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

function codeProfile {
    code $PROFILE
}

function pull {
    param (
        [string]$branch
    )

    $initialBranch = git rev-parse --abbrev-ref HEAD

    if ([string]::IsNullOrEmpty($branch)) {
        $branch = $initialBranch
    } else {
        git checkout $branch
    }

    git fetch
    git pull origin $branch
    git status

    if (-not [string]::IsNullOrEmpty($branch) -and $branch -ne $initialBranch) {
        git checkout $initialBranch
    }
}
```
Open Powershell in admin, then copy/paste and select 1 and restart windows
```
$mode = Read-host "How do you like your mouse scroll (0 or 1)?"; Get-PnpDevice -Class Mouse -PresentOnly -Status OK | ForEach-Object { "$($_.Name): $($_.DeviceID)"; Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters" -Name FlipFlopWheel -Value $mode; "+--- Value of FlipFlopWheel is set to " + (Get-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters").FlipFlopWheel + "`n" }
```

To investigate
=> http://jagt.github.io/clumsy/index.html
=> https://github.com/stevenilsen123/mac-keyboard-behavior-in-windows
