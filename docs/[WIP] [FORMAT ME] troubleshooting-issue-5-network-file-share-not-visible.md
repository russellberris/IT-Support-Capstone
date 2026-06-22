my shared folder i created in my server VM is not showing up on either of my machines' File explorer > network. what do?

1
If your shared folder is not appearing in the "Network" section of File Explorer, it is almost always due to Network Discovery settings or the Server Message Block (SMB) protocol not being properly advertised in the local network environment.
Windows Server and client machines often have these features off by default for security. You must ensure this is active on both the Server and the client machines.

Open Control Panel > Network and Sharing Center > Change advanced sharing settings.
Ensure Network discovery is Turned on.
Ensure File and printer sharing is Turned on.
Do this on both the Server VM and the local client machine you are trying to connect from.

[DONE - NETWORK DISCOVERY WAS OFF IN SERVER VM - TURNED IT ON - STILL NOT VISIBLE]

2
Verify the "Function Discovery" Services
Even with settings turned on, Windows needs background services to "announce" that the server is there. If these aren't running, the server won't show up in the Network list.

On the Server VM, press Win + R, type services.msc, and hit Enter.
Find these two services:
Function Discovery Provider Host
Function Discovery Resource Publication
Right-click each, select Properties, change the Startup type to Automatic, and then click Start.
Restart the Server and check the client machine again.

[DID THIS - PROVIDER HOST WAS RUNNING, RESOURCE PUBLICATION WAS NOT]
[SRV MACHINE STILL NOTHING ON SHARE - CLIENT MACHINE HAS A SHARED PC WITH A STRANGE NAME - WIN-U3750GKU05D]
[AFTER CHANGING THE "MUST CHANGE PASSWORD AT FIRST LOGON" POLICY IN ADUC ON SERVER VM, SHARE IS NOW VISIBLE IN CLIENT VM]

3
Check Firewall Rules
The Windows Firewall often blocks the traffic required for the "Network" browser to function.
On the Server, open Windows Defender Firewall with Advanced Security.
Go to Inbound Rules.
Ensure that the rules for File and Printer Sharing (SMB-In) are enabled for your active network profile.
[DONE - LOOKS GOOD]

4
Waiting for Windows "Network Discovery" to populate can take 15–20 minutes and is notoriously unreliable in virtual environments. You do not actually need it to show up in the list to use the folder.
Instead of browsing, use the direct network path:
On your client machine, press Win + R.
Type \\<Server-IP-Address> (e.g., \\192.168.1.50).
Hit Enter.
This will bypass the "Network" discovery service entirely and connect you directly to the server's shares.
[DID IT ON CLIENT VM - WORKED!]
[FILE SHARES ARE ONLY VISIBLE ON CLIENT BUT THAT MAY BE ENOUGH TO PROCEED WITH PROJECT - WILL CHECK AND REPORT BACK TO THIS DOC]

