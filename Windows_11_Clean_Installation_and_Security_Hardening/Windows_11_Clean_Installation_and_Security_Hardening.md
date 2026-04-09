# Windows 11 Clean Installation & Security Hardening

## Objective

Perform a clean installation and security hardening of Windows 11 Pro on a Dell Latitude 7400 by reinstalling from bootable external media, applying essential security settings, and verifying system security.

## Environment

- Device: Dell Latitude 7400
- Operating System: Windows 11 Pro 10.0.26200
- CPU: Intel(R) Core(TM) i7-8665U CPU @ 1.90GHz
- RAM: 16 GB
- Storage: 512 GB
- BIOS: Dell Inc. 1.40.1, 4/18/2025
- System Type: x64-based PC
- Tools: PowerShell, DiskPart, Windows Media Creation Tool, Bootable USB Drive, Windows Update, Device Manager, Windows Security, BitLocker, Event Viewer

<img src="Screenshots/Environment/environment_03.png" width="413px" alt="system information">
<img src="Screenshots/Environment/environment_01.png" width="413px" alt="processor information">
<img src="Screenshots/Environment/environment_02.png" width="413px" alt="system drive information">

## Phase 1: Pre-Checks

- Verified Windows edition and activation status to confirm Windows will reactivate automatically after installation.

<img src="Screenshots/Phase_1_Pre-checks/Phase_1_02.png" width="620" alt="Windows activation status">

- Checked BitLocker status and backed up recovery key to prevent potential lockout or data loss and protect against unexpected scenarios during the installation process.

<img src="Screenshots/Phase_1_Pre-checks/Phase_1_03.png" width="413" alt="BitLocker status">

- Identified disk layout to understand how storage was partitioned and to ensure the correct drive and partitions were selected and removed during the installation process.

<img src="Screenshots/Phase_1_Pre-checks/Phase_1_04.png" width="413" alt="system disk information">
<img src="Screenshots/Phase_1_Pre-checks/Phase_1_05.png" width="620" alt="disk partition information">

## Phase 2: Backup

- Used `robocopy` in PowerShell to back up my IT projects folder to an external drive before the clean installation to ensure all project data was preserved and could be restored after the system rebuild.

<img src="Screenshots/Phase_2_Backup/Phase_2_01.png" width="620" alt="robocopy backup command">
<img src="Screenshots/Phase_2_Backup/Phase_2_02.png" width="413" alt="backup confirmation">

- Verified backup integrity by accessing files on the external device.

<img src="Screenshots/Phase_2_Backup/Phase_2_03.png" width="620" alt="backed up data in File Explorer">

## Phase 3: Create Bootable USB

- Used `diskpart` to fully wipe a USB drive for use as an installation device.

<img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_01.png" width="413" alt="USB wipe and confirmation">

- Downloaded the Windows Media Creation Tool from Microsoft’s Windows 11 download page and ran MediaCreationTool.exe to launch the utility and begin creating the Windows 11 installation media.

<img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_02.png" width="620" alt="Windows Media Creation Tool download page">

> ### ⚠️ Issue Encountered: Media Creation Tool could not detect USB drive
>
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_03.png" width="620" alt="missing USB drive">
>
> - Verified USB drive was detected by Windows and had a drive letter assigned.
>
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_09.png" width="413" alt="USB drive in File Explorer">
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_05.png" width="620" alt="USB drive in Disk Management">
>
> - Clicked on the USB drive in File Explorer and a dialog displayed that read "You need to format the disk in drive D: before you can use it."
>
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_04.png" width="413" alt="disk format dialog">
>
> - Attempted to format the USB drive from the File Explorer dialog but Windows displayed an error indicating it could not format drive D:.
>
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_08.png" width="207" alt="disk format configuration">
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_10.png" width="413" alt="disk format error dialog">
>
> ### ✅ Resolution
>
> - Used `diskpart` to clean the USB drive and successfully format it with a new filesystem. The USB drive then appeared in the Microsoft Media Creation Tool.
>
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_06.png" width="310" alt="diskpart USB drive format">
><img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_07.png" width="620" alt="USB drive in Media Creation Tool">
>
- Created Windows 11 installation files using the Media Creation Tool, and the USB drive was successfully configured as bootable installation media.

<img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_12.png" width="310" alt="bootable drive confirmation">
<img src="Screenshots/Phase_3_Create_Bootable_USB/Phase_3_13.png" width="516" alt="bootable drive contents in File Explorer">

## Phase 4: Clean Installation

- Booted into the UEFI boot menu and selected the Windows 11 installation USB.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_01.JPG" width="516" alt="UEFI boot menu">

- Chose the "Install Windows 11" option in Windows Setup to do a clean installation.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_03.JPG" width="516" alt="Windows setup options">

- Deleted all existing partitions on the internal SSD.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_04.JPG" width="516" alt="disk partitions">
<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_08.JPG" width="516" alt="deleted disk partitions">

- Launched the Windows 11 Pro installation process. Windows recreated the necessary partitions.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_09.JPG" width="516" alt="ready to install">
<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_18.png" width="516" alt="disk partitions in Disk Management">

- Configured country and keyboard layout, created a strong and unique PIN for my system, and selected the option to "Set up as a new PC" to start my system with baseline settings.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_11.JPG" width="413" alt="select country">
<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_12.JPG" width="413" alt="select keyboard">

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_15.JPG" width="413" alt="PIN setup">
<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_16.JPG" width="413" alt="new installation setup">

- Successfully completed the Windows 11 Pro installation and the system booted properly into the new operating system.

<img src="Screenshots/Phase_4_Clean_Installation/Phase_4_17.JPG" width="620" alt="fresh installation Start menu and desktop">

## Phase 5: Post-Installation Baseline

- Ran Windows Update repeatedly until no further updates were available and restarted the system after updates to ensure the installation was fully patched.

<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_01.png" width="516" alt="available Windows updates">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_02.png" width="413" alt="available Windows updates">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_03.png" width="310" alt="Windows up-to-date confirmation">

- Verified Windows activation and confirmed the system successfully reactivated after the installation using the existing digital license.

<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_04.png" width="620" alt="Windows activation status">

- Used Device Manager to verify that no devices were reporting errors or missing drivers. There were no warning indicators and system hardware was recognized.

<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_06.png" width="310" alt="Device Manager listings">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_07.png" width="310" alt="Device Manager listings">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_08.png" width="310" alt="Device Manager listings">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_09.jpg" width="310" alt="Device Manager listings">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_10.png" width="310" alt="Device Manager listings">
<img src="Screenshots/Phase_5_Post_Installation_Baseline/Phase_5_11.png" width="310" alt="Device Manager listings">

## Phase 6: Security Hardening & Verification

### Hardening

- Enabled BitLocker on the system drive to encrypt data at rest and backed up the recovery key during setup.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_04.png" width="516" alt="BitLocker off">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_10.png" width="516" alt="BitLocker on">

- Booted into the UEFI firmware settings and enabled Secure Boot to help prevent unauthorized or untrusted bootloaders and low-level malware from loading during system startup.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_31.png" width="413" alt="System Information Secure Boot off">

<img src="Screenshots\Phase_6_Security_Hardening\Phase_6_33.JPG" width="310" alt="UEFI settings menu">
<img src="Screenshots\Phase_6_Security_Hardening\Phase_6_34.JPG" width="310" alt="Secure Boot disabled">
<img src="Screenshots\Phase_6_Security_Hardening\Phase_6_35.JPG" width="310" alt="Secure Boot enabled">

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_32.png" width="413" alt="System Information Secure Boot on">

- Ensured that Microsoft Defender real-time protection, cloud-delivered protection, and tamper protection were enabled to detect and block threats in real time, improve response to newly identified threats, and help prevent security settings from being disabled or altered.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_11.png" width="413" alt="Windows Security settings">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_12.png" width="413" alt="Windows Security settings">

- Enabled ransomware protection by turning on Controlled folder access in Windows Security to help prevent unauthorized applications from modifying or encrypting protected files and folders.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_16.png" width="413" alt="ransomware protection off">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_17.png" width="413" alt="ransomware protection on">

- Created a separate standard user account for everyday use and kept an administrator account for system changes and other elevated tasks to reduce the risk of unauthorized system changes and limit the impact of malicious software during normal use.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_18.png" width="413" alt="user accounts menu">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_21.png" width="413" alt="user accounts menu new user added">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_01.png" width="413" alt="admin and standard user accounts">

- Enabled all protections in Windows Security's Reputation-based protection settings, including Check apps and files, SmartScreen for Microsoft Edge, Phishing protection, Potentially unwanted app blocking, and SmartScreen for Microsoft Store apps to protect against malicious downloads, unsafe websites, phishing attempts, and suspicious applications.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_23.png" width="413" alt="Reputation-based protection settings">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_24.png" width="413" alt="Reputation-based protection settings">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_25.png" width="413" alt="Reputation-based protection settings">

### Verification

- Verified BitLocker status in PowerShell using `manage-bde -status` to confirm that encryption was complete and protection status was active.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_26.png" width="413" alt="BitLocker status">

- Verified Microsoft Defender status using `Get-MpComputerStatus` to confirm that antivirus protections were enabled and functioning properly.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_27.png" width="516" alt="Microsoft Defender status">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_28.png" width="516" alt="Microsoft Defender status">

- Verified that Windows Firewall was enabled by checking the firewall profiles with `Get-NetFirewallProfile` to confirm that network traffic filtering protections were active after configuration.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_29.png" width="516" alt="Windows Firewall status">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_30.png" width="516" alt="Windows Firewall status">

- Reviewed Event Viewer logs, including the System and Application logs, after installation and security hardening to check for major system, security, or hardware-related issues that might indicate unresolved problems after deployment. No major issues were identified.

<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_02.png" width="620" alt="Event Viewer logs">
<img src="Screenshots/Phase_6_Security_Hardening/Phase_6_03.png" width="620" alt="Event Viewer logs">

## Results

This project resulted in a successful clean installation of Windows 11 Pro on the Dell Latitude 7400. The system was fully updated and properly activated with the existing license. Device Manager showed no missing drivers or device errors.

Core security protections were applied and verified, including BitLocker, Secure Boot, Microsoft Defender, Windows Firewall, ransomware protection, and reputation-based protection settings. A separate standard user account was also created for everyday use, with the administrator account reserved for elevated tasks.

Final verification confirmed a clean, fully functional, and security-hardened Windows 11 system with a stronger security posture than the original default setup.

## Takeaways

- A clean installation provides a known starting point by removing clutter, unnecessary software, and unknown configuration issues.

- After enabling security settings, it's important to verify that protections are active.

- Built-in Windows tools such as BitLocker, Microsoft Defender, Windows Firewall, Device Manager, PowerShell, and Event Viewer can be used to establish and verify solid baseline security.

- Using a standard user account for everyday activity helps improve security by separating normal use from administrative access.

- Documenting each phase of the process makes the work easier to review, communicate, and repeat.
