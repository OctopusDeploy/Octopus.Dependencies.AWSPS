**Note: Octopus no longer bundles these tools directly into Octopus Server. Follow the below steps if you are still relying on the AWSPowerShell Module in your Octopus Deploy scripts**

# Octopus.Dependencies.AWSPS
This project downloads the AWS PowerShell modules and repacks them into a NuGet package.

## Maually Installing AWSPowershell Module
We reccomend following the [official AWS guides](https://docs.aws.amazon.com/powershell/v4/userguide/pstools-getting-set-up-windows.html) for installing the AWSPowerShell Modules for Windows. 
Since this installation uses the built in PowerShell commands, you may require Administrator Rights to perform.

### Installing Globally


```PowerShell
Install-Module -Name AWSPowerShell

# Uninstall using the below
# Uninstall-Module -Name AWSPowerShell -AllVersions
```
We reccomend installing AWSPowerShell on your target to avoid relying on downloading it on every step invocation as described in the `Installation to Deployment Session` option below.

### Installation to Deployment Session
If you are unable to install AWSPowerShell on your target directly, you may be able to include the below script directly into the top of your Octopus AWS Script Step.

The version described in this script snippet is the last version that was bundled with Octopus Server. 
We reccomend downloading the latest version that is available, however note that as the later versions are much larger, this import process will take much longer.

```PowerShell
$AWSPowerShellVersion="3.3.390.0" # We reccomend installing the latest version
Write-Host Downloading AWSPowerShell v$AWSPowerShellVersion Module locally
Save-Module -Name AWSPowerShell -Path .\  -RequiredVersion $AWSPowerShellVersion
Write-Host Importing AWSPowerShell Module into local session
Import-Module -DisableNameChecking ".\AWSPowerShell\$AWSPowerShellVersion\AWSPowerShell.psd1"


```
The reccomended mechanism
