# Windows Containers on Windows Server

This exercise walks through basic deployment and use of the Windows container feature on Windows Server 2016. During this exercise, you install the container role and deploy a simple Windows Server container. If you need to familiarize yourself with containers, you can find this information in [About Containers](https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/index).

This quick start is specific to Windows Server containers on Windows Server 2016. Additional quick start documentation, including containers in Windows 10, are found in the table of contents on the left hand side of this page.

### Prerequisites:

One computer system (physical or virtual) running Windows Server 2016. If you are using Windows Server 2016 TP5, please update to Window Server 2016 Evaluation.

Critical updates are needed in order for the Windows Container feature to function. Please install all updates before working through this tutorial.

If you would like to deploy on Azure, this template makes it easy.
 

## 1. Install Docker

To install Docker we'll use the OneGet provider PowerShell module which works with providers to perform the installation, in this case the MicrosoftDockerProvider. The provider enables the containers feature on your machine. You also install Docker which requires a reboot. Docker is required in order to work with Windows containers. It consists of the Docker Engine and the Docker client.

Open an elevated PowerShell session and run the following commands.

First, install the Docker-Microsoft PackageManagement Provider from the [PowerShell Gallery](https://www.powershellgallery.com/packages/DockerMsftProvider).

```PowerShell
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
```

Next, you use the PackageManagement PowerShell module to install the latest version of Docker.

```PowerShell
Install-Package -Name docker -ProviderName DockerMsftProvider
```

When PowerShell asks you whether to trust the package source 'DockerDefault', type ```A``` to continue the installation. When the installation is complete, reboot the computer.

```PowerShell
Restart-Computer -Force
```

```Tip: If you want to update Docker later:```

* Check the installed version with
```PowerShell
Get-Package -Name Docker -ProviderName DockerMsftProvider
```
* Find the current version with
```PowerShell
Find-Package -Name Docker -ProviderName DockerMsftProvider
```
* When you're ready, upgrade with
```PowerShell
Install-Package -Name Docker -ProviderName DockerMsftProvider -Update -Force
```
followed by
```PowerShell
Start-Service Docker
```

## 2. Install Windows Updates

Ensure your Windows Server system is up-to-date by running:

```Batchfile
sconfig
```

This shows a text-based configuration menu, where you can choose option 6 to Download and Install Updates:

```Batchfile
===============================================================================
                         Server Configuration
===============================================================================

1) Domain/Workgroup:                    Workgroup:  WORKGROUP
2) Computer Name:                       WIN-HEFDK4V68M5
3) Add Local Administrator
4) Configure Remote Management          Enabled

5) Windows Update Settings:             DownloadOnly
6) Download and Install Updates
7) Remote Desktop:                      Disabled
...
```

When prompted, choose option A to download all updates.

## 3. Deploy Your First Container

For this exercise, you download a pre-created .NET sample image from the Docker Hub registry and deploy a simple container running a .Net Hello World application.

Use ```docker run``` to deploy the .Net container. This will also download the container image which may take a few minutes.

```Batchfile
docker run microsoft/dotnet-samples:dotnetapp-nanoserver
```

The container starts, prints the hello world message, and then exits.

```Batchfile
         Dotnet-bot: Welcome to using .NET Core!
    __________________
                      \
                       \
                          ....
                          ....'
                           ....
                        ..........
                    .............'..'..
                 ................'..'.....
               .......'..........'..'..'....
              ........'..........'..'..'.....
             .'....'..'..........'..'.......'.
             .'..................'...   ......
             .  ......'.........         .....
             .                           ......
            ..    .            ..        ......
           ....       .                 .......
           ......  .......          ............
            ................  ......................
            ........................'................
           ......................'..'......    .......
        .........................'..'.....       .......
     ........    ..'.............'..'....      ..........
   ..'..'...      ...............'.......      ..........
  ...'......     ...... ..........  ......         .......
 ...........   .......              ........        ......
.......        '...'.'.              '.'.'.'         ....
.......       .....'..               ..'.....
   ..       ..........               ..'........
          ............               ..............
         .............               '..............
        ...........'..              .'.'............
       ...............              .'.'.............
      .............'..               ..'..'...........
      ...............                 .'..............
       .........                        ..............
        .....


**Environment**
Platform: .NET Core 1.0
OS: Microsoft Windows 10.0.14393
```

For in depth information on the Docker Run command, see Docker Run Reference on Docker.com.