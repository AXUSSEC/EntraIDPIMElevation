# EntraIDPIMElevation

## Get the repo

Go to where you want the repo to be cloned to

```bash
cd ~\Documents\MyRepos\
```

Use `git clone` to [clone](https://git-scm.com/docs/git-clone) the repo

```bash
git clone https://github.com/Anticimex-USA/EntraIDPIMElevation.git
```

## Consent to permissions

`cd` to the repo and run

```PowerShell
.\invoke-EntraIDPimElevations.ps1 -Consent
```

Sign into the account whose groups you want to activate, and send a request to the admins to consent to the delegated permissions.

## Using the repo

***WARNING: Please take care to only use this for everyday roles and avoid using it for more privileged roles like Security Admin and Exchange Admin. This would defeat the purpose of PIM and your admin will be displeased.***

Below is an example that, once added to your [PowerShell profile](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.4), if you run 

```PowerShell
PIMRoles
``` 

The following will happen:

- Groups `Group 1`,`Group 2`,...,`Group 5` will be activated as a `member` 
- The above activation will last for 4 hours
- A justification of "Daily support" will be logged
- The logon context will refresh after activation

```PowerShell
function PIMRoles {
    $PIMScriptPath = "C:\Path\to\script"
    # The script requires a *single* string of groups separated by commas.
    $Groups = @(
        "Group 1"
        "Group 2"
        "Group 3"
        "Group 4"
        "Group 5"
    )
    $GroupString = $Groups -join ","

    $params = @{
        GroupsToActivate = $GroupString 
        Justification = "Daily support" 
        AccessType = "Member"
        ActivationDuration = 4
        ForceRefresh = $true
    }

    . $PIMScriptPath @params
}
```

Use 

```PowerShell
Get-Help -Full .\invoke-EntraIDPimElevations.ps1
```

for more info on usage.