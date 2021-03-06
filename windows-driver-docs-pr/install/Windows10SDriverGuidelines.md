# Windows 10 S Driver Guidelines


This section provides an overview of the code integrity policy, which hardware
and software drivers are subject to when installed on Windows 10 S. This section
also provides an overview of the requirements for drivers intended to run on
Windows 10 S.

Code integrity policy overview
------------------------------

-   All executable code must be signed with a **Windows, WHQL, ELAM, or Store**
    certificate.

-   All Windows 10 kernel mode drivers must be submitted to the Windows Hardware
    Developer Center Dashboard portal (Dev Portal) to be digitally signed by
    Microsoft.

-   Windows 10 will not load any kernel mode drivers which are not signed by
    using one of the methods above.

-   All companion software must be signed using one of the above methods.

-   Only runs trusted apps from the Windows Store.

-   Policy is enforced in the CreateProcess API, via code integrity checks that
    check if the code that is about to execute is signed with a valid
    certificate.

-   Any unsigned code results in user notification, informing them and helping
    them find what they need.

### Blocked inbox components 

As part of Windows 10 S code integrity, the following components are blocked
from executing.

-   bash.exe

-   cdb.exe

-   cmd.exe

-   cscript.exe

-   csi.exe

-   dnx.exe

-   kd.exe

-   lxssmanager.dll

-   msbuild.exe

-   ntsd.exe

-   powershell.exe

-   powershell\_ise.exe

-   rcsi.exe

-   reg.exe

-   regedt32.exe

-   windbg.exe

-   wmic.exe

-   wscript.exe

### Driver Guidelines

For drivers to install and run successfully on Windows 10 S, the following must
be met.

-   All driver packages and binaries must be digitally signed by Microsoft
    through Dev Center - [aka.ms/DevCenterPortal](aka.ms/DevCenterPortal)

-   Driver packages may not contain any archives that extract nested binaries
    which are not signed.

    -   Do not include an \*.exe, \*.zip, \*.msi or \*.cab in the driver package
        that extracts any binaries that are not WHQL signed.

    -   Drivers should be installed using only INF directives

    -   Co-installers may be used only for the purpose of installing or
        registering signed binaries, and may not contain any UI components

    -   Drivers may not make calls to [blocked inbox
        components](#blocked-inbox-components).

-   Drivers may not include any 3rd party UI components, apps, or settings.
    Instead Universal applications from the Windows Store should be provided for
    user interfaces and may also leverage Settings app extensibility. (eg;
    Hardware Support Apps, Windows Store Device Apps, Centennial Apps using
    Desktop Bridge)

-   All driver and firmware servicing must use Windows Update (no support for
    3rd party updater apps)

-   Where possible, use a Universal Driver.

    -   <https://msdn.microsoft.com/en-us/windows/hardware/drivers/develop/getting-started-with-universal-drivers>

    -   <https://msdn.microsoft.com/en-us/windows/hardware/drivers/develop/validating-universal-drivers>
