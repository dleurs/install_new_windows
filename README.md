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

function push {
    param (
        [string]$branch,
        [switch]$forceWithLease
    )

    # Get the current branch if none is provided
    $initialBranch = git rev-parse --abbrev-ref HEAD

    if ([string]::IsNullOrEmpty($branch)) {
        $branch = $initialBranch
    }

    # Check if the branch is valid
    if (-not (git branch --list $branch)) {
        Write-Host "Error: Branch '$branch' does not exist." -ForegroundColor Red
        return
    }

    # Prepare the push command
    $pushCommand = "git push origin $branch"
    if ($forceWithLease) {
        $pushCommand += " --force-with-lease"
    }

    # Execute the push command
    Invoke-Expression $pushCommand
}
```
Open Powershell in admin, then copy/paste and select 1 and restart windows
```
$mode = Read-host "How do you like your mouse scroll (0 or 1)?"; Get-PnpDevice -Class Mouse -PresentOnly -Status OK | ForEach-Object { "$($_.Name): $($_.DeviceID)"; Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters" -Name FlipFlopWheel -Value $mode; "+--- Value of FlipFlopWheel is set to " + (Get-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Enum\$($_.DeviceID)\Device Parameters").FlipFlopWheel + "`n" }
```

To investigate
=> http://jagt.github.io/clumsy/index.html
=> https://github.com/stevenilsen123/mac-keyboard-behavior-in-windows
