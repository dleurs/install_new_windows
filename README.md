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
