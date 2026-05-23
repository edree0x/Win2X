sfc /scannow
DISM /Online /Cleanup-Image /RestoreHealth
DISM /Online /Cleanup-Image /StartComponentCleanup
chkdsk C: /scan /forceofflinefix
bootrec /rebuildbcd
netsh winsock reset
ipconfig /flushdns
cleanmgr /sagerun:1
del /s /f /q C:\Windows\Prefetch\*.* >nul 2>&1
del /s /f /q C:\Windows\Temp\*.* >nul 2>&1
del /s /f /q "%USERPROFILE%\AppData\Local\Temp\*.*" >nul 2>&1
wsreset -i
PowerShell -Command "[System.GC]::Collect(); [System.GC]::WaitForPendingFinalizers();"
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection" /v AllowTelemetry /t REG_DWORD /d 0 /f >nul 2>&1
sc config DiagTrack start= disabled >nul 2>&1
sc stop DiagTrack >nul 2>&1
powercfg /duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61 | powercfg /setactive e9a42b02-d5df-448d-aa00-03f14749eb61 >nul 2>&1
taskkill /f /im explorer.exe >nul 2>&1
start explorer.exe