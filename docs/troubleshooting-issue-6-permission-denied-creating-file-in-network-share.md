trying to create a .txt in network shared folder from the server VM, got permission denied popup, i modified folder options to allow ful control, popup still happening, what do

1
When you encounter "Access Denied" errors on a network share despite granting "Full Control," the issue is almost always caused by a mismatch or conflict between the two distinct layers of Windows permissions: Share Permissions and NTFS Permissions.
Both layers must allow access; the most restrictive setting between the two will win.

To fix this, you must ensure your user account has explicit "Allow" permissions in BOTH locations:

a Check Share Permissions: Right-click the folder > Properties > Sharing tab > Advanced Sharing > Permissions. Ensure your user or group is listed here with "Full Control" or "Change" checked.
b Check NTFS Permissions: Right-click the folder > Properties > Security tab. Ensure your user or group is listed here with "Modify" or "Full Control" checked. 

[TRIED A, DID NOT SEE THE SHARING TAB]
back up, when i go to check share permissions, there is no sharing tab under properties, what do i do

If the Sharing tab is missing from the Properties window, it usually indicates that you are either not looking at the parent folder that is actually shared, or that the Server service is not running on the machine hosting the files.

2
Press Win + R, type services.msc, and hit Enter.
Scroll down to the Server service.
Check the "Status" column. It should say Running.
If it is not running, right-click it and select Start.
If it is already running, right-click and select Restart.
Once verified, go back to your folder properties; the Sharing tab should now appear.

[DID IT, IT WAS RUNNING]

3
In some enterprise or locked-down environments, administrators use Group Policy to prevent users from creating new shares or modifying existing ones.
Check: If you are an administrator and the Server service is running, but the tab is still missing, open the Command Prompt as an administrator and type:
net share
This command will list all active shares on the system. If your folder is listed here, it is shared. If it is not listed, the folder is not shared, and you cannot manage it via the Sharing tab because it doesn't exist as a network share yet.

[FOLDER IS LISTED BUT I WANT TO CREATE A TEXT FILE I DON'T WANT TO SEE IF STATUS IS SET TO SHARED]

i am trying to create a .txt inside a network share folder. why is net share info relevant here

The reason I suggested checking net share is that if a folder isn't officially registered as a "share" by the Windows operating system, it cannot be accessed over the network, regardless of what your NTFS (Security) permissions say.

If you are looking at the properties of a folder and the Sharing tab is gone, that specific folder is not the "root" of the share. In Windows, you can only set share-level permissions on the folder that was originally shared. Any subfolders inside it inherit those permissions automatically, and they do not show a Sharing tab because they are not individually shared.

If you cannot find the parent folder to change the permissions, you can use the Computer Management console to see exactly where the share starts:

Open Computer Management (Right-click the Start button > Computer Management).
Navigate to System Tools > Shared Folders > Shares.
Look at the list. Find the path that corresponds to the location you are trying to reach.
Example: You might be trying to write to \\Server\Data\Projects\Work, but the Share was actually created at \\Server\Data.
Because the share starts at \Data, the \Projects and \Work folders will not have a Sharing tab.

[DID IT, REALIZED THE FOLDERS ARE IN C: SO NEED TO CHANGE PERMISSIONS THERE]

Identify the Root: In that Computer Management list, find the "Path" column. That is the folder where you must go to change the Share permissions.

Verify the User: Once you find the root folder path, go to that folder in File Explorer, right-click it, and look for the Sharing tab there.

Check Permissions: Ensure your user account is listed in the Sharing tab > Permissions button with "Change" or "Full Control" checked.

Confirm NTFS: Even if you fix the Sharing tab, go back to the folder where you are actually trying to create the .txt file, right-click it, go to the Security tab, and ensure your user has "Modify" permissions there as well.

[WENT TO C: INSTEAD TO SEE IF SHARING TAB VISIBLE AT THAT LOCATION]
[IT WAS! HOORAY!]

[CONTINUED WITH PROJECT ON PAGE 73 STEP 67 OF LUKE'S PHASE 1 PDF]










