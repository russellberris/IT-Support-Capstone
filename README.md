# IT-Support-Capstone
Russell Berris's Per Scholas Houston (cohort 2026-HOU-01) final capstone project.  Involved five phases: 
1) Setting up and migrating a Windows server machine and a Windows client machine
2) Purposely "breaking" the environment using provided PowerShell scripts that altered configurations and settings
3) Documenting what was broken via provided incident tickets
4) Resolving all incident tickets and restoring full system functionality with verification testing
5) Concluding reflections and lessons learned.

Click here to view the full Technical Report: ([Russell Berris.Capstone.PDF](https://github.com/russellberris/IT-Support-Capstone/blob/main/Russell%20Berris.Capstone.pdf))

## Executive Summary: Migration & Stabilization Event

This technical report details the execution of an IT infrastructure project involving the setup, migration, and stabilization of a Windows-based enterprise environment. The project was completed using a virtualization approach, utilizing VirtualBox to host two virtual machines: a Windows Server 2022 instance (MIG-SRV01) and a Windows 11 client instance (MIG-CLI01).  

Key achievements of this project include:

- <ins>Environment Baseline:</ins> Successful configuration of a virtualized domain environment, including the installation of Windows Server and Windows 11, and the establishment of internal network connectivity between the machines. 

- <ins>Active Directory & Access Control:</ins> Deployment of Active Directory Domain Services (AD DS) on the server, domain joining of the client machine, and the implementation of role-based file access permissions within a shared network folder.  

- <ins>Incident Response & Stabilization:</ins> Execution of a migration event followed by a structured incident response phase, addressing common post-migration issues such as connectivity, printer availability, and system performance.  

- <ins>System Verification:</ins> Implementation and documentation of automated PowerShell verification scripts to ensure the integrity and stability of the environment across all project phases.  This project provided hands-on experience in managing enterprise infrastructure, troubleshooting complex service dependencies, and applying AI-assisted support methodologies to stabilize system environments.
