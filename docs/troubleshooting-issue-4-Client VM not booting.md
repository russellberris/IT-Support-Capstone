Day 3 - 6/20/26 2:40pm Issue #4
## Problem
A Windows 11 virtual machine (VM) in VirtualBox failed to boot, remaining stuck on a black screen despite being reported as "Running." This issue occurred in an environment where a Windows Server 2022 VM was already functioning correctly, indicating that the host's virtualization infrastructure was stable but the specific Windows 11 VM configuration was incompatible.

## Root Cause/Diagnosis
Eureka! It worked. 🥳 
The issue was identified as a display configuration incompatibility. Windows 11 has stricter hardware and display requirements than Windows Server 2022, particularly with graphics driver compatibility within VirtualBox. While virtualization prerequisites (TPM 2.0 and Secure Boot) were correctly configured, the default Graphics Controller setting (`VBoxVGA`) was incompatible with the Windows 11 guest environment, resulting in a black screen during boot.

## Resolution
The problem was resolved by adjusting the VM's display settings:
1.  **Checklist of Settings:** The following configuration was verified:
    * **Processors:** Assigned 2+ cores [X]
    * **TPM:** Set to v2.0 [X]
    * **Secure Boot:** Enabled [X]
    * **3D Acceleration:** Disabled [X]
2.  **Display Configuration:** Navigated to **Settings > Display > Screen**.
3.  **Graphics Controller Change:** The controller was manually switched from the default `VBoxVGA` to `VMSVGA`. This change allowed the VM to properly interface with the virtualized display hardware, successfully allowing the boot process to complete. This was a specific setting adjustment that would not have been identified without online guidance. 


## *Lessons Learned*
* <ins>**Consultation Accelerates Troubleshooting</ins> -** Asking the right questions in my online guidance allowed for the identification of a specific, non-obvious setting (the Graphics Controller) that resolved the issue in a few minutes.
* <ins>**Systematic Verification is Essential</ins> -** Creating a checklist of prerequisites (TPM, Secure Boot, CPU allocation) ensures that foundational requirements are met before testing specific variables like display controllers.
* <ins>**Graphics Controller Sensitivity</ins> -** Different guest operating systems in VirtualBox have varying dependencies for display drivers; switching from legacy controllers (VBoxVGA) to modern ones (VMSVGA) is a critical step when debugging black-screen boot failures.
* <ins>**Scope Application</ins> -** The method of logically rooting out the issue by isolating variables (verifying that other VMs work to rule out host issues, then methodically testing specific configuration settings) is a valuable troubleshooting skill for any professional IT Support environment.
