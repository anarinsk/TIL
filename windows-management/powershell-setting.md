# Powershell 설정 

- 기본 설정 파일의 위치는 다음과 같다. 
```
C:\Users\junsokhuhh\Documents\PowerShell\profile.ps1 
```
- 터미널에 보통 자세히 표시된다. 

# Profile 

- 위 디렉토리에 있는 `.ps1` 파일은 다 설정에 포함되는 듯. 

## `Microsoft.PowerSHell_profile.ps1`

```shell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression
#oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\bubbles.omp.json" | Invoke-Expression
#oh-my-posh init pwsh --config "$Home\pwsh10k.omp.json" | Invoke-Expression
#oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\agnosterplus.omp.json" | Invoke-Expression
#oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\agnoster.omp.json" | Invoke-Expression
#oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\iterm2.omp.json" | Invoke-Expression
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\powerlevel10k_modern.omp.json" | Invoke-Expression
```
- oh-my-posh 설정 

## `profile.ps1`

```shell
#region conda initialize
# !! Contents within this block are managed by 'conda init' !!
If (Test-Path "C:\Users\junsokhuhh\Miniconda3\Scripts\conda.exe") {
    (& "C:\Users\junsokhuhh\Miniconda3\Scripts\conda.exe" "shell.powershell" "hook") | Out-String | ?{$_} | Invoke-Expression
}
#endregion

# Personal setting 

cd e:/github
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmen
```
