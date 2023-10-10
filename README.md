# WInget installation

On many of my Windows systems is no winget installed and i have spend a lot of time to get them ready for use.

Downlaod the latest Version of die Windows Desktop Installer from https://github.com/microsoft/winget-cli/releases/latest 

Clone this repo and execute the following code in PowerShell as Administrator

```pwsh
# Enable TLS 1.2 for this session in-case disabled on machine
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

# Install NuGet Package Provider. For future use
Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
# Install Package Provider Source. For future use
Register-PackageSource -provider NuGet -name nugetRepository -location https://www.nuget.org/api/v2
#Install Prerequisites for WinGet
Install-Package Microsoft.UI.Xaml -Force
Install-Module -Name Microsoft.WinGet.Client

# Install Requirements
Add-AppxPackage %userprofile%\Downloads\Microsoft.UI.Xaml.2.7_8wekyb3d8bbwe.Appx
Add-AppxPackage %userprofile%\Downloads\Microsoft.VCLibs.140.00.UWPDesktop_8wekyb3d8bbwe.Appx
# Install DesktopAppInstaller (winget)
Add-AppxProvisionedPackage -Online -PackagePath %userprofile%\Downloads\Microsoft.DesktopAppInstaller_*.msixbundle -LicensePath %userprofile%\Downloads\*_License1.xml
# Install winget package source
Add-AppxPackage %userprofile%\Downloads\Winget_Source.msix

# Install Choco
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
