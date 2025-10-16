<p align="center">
<img width="1200" height="630" alt="File shares" src="https://github.com/user-attachments/assets/2d2ee3f6-7059-4634-9538-0751e3e50639" />

</p>

<h1>Network File Shares and Permissions (Azure)</h1>
This tutorial outlines the implementation of Network File Shares and Permissions in Azure<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Step 1: Logging into to our DC-1 (Domain Controller) Virtual Machine in Azure</h2>
<b>Log into the domain controller as Jane Admin</b>
<img src="https://i.imgur.com/8oziyjU.png" width="600" alt="NFS"/>
<br />


<h2>Step 2: Create Folders in File explorer</h2>
<b>We will create four folders</b>
<ul>
  <li>The first file name will be read-access</li>
  <li>Second will be write-access</li>
  <li>Third will be No-access</li>
  <li>Fourth will be accounting</li>
  <img src="https://i.imgur.com/OaXq7r7.png" width="600" alt="NFS"/>
</ul>
<br />


<h2>Step 3: Give the "read-access" Folder read permission level</h2>
<b>Allow the team announcements folder only read permissions for the domain users</b>
<p>
  <ul>
    <li>Right click the folder > Select Properties</li>
    <li>Click the Sharing tab</li>
    <li>Next click the share button</li>
    <img src="https://i.imgur.com/B2hYdXV.png" width="600" alt="NFS"/>
    <li>Type Domain Users</li>
    <li>Click Add</li>
    <img src="https://i.imgur.com/zm44PJB.png" width="600" alt="NFS"/>
    <li>Set the Permission level for the Domain Users to Read</li>
    <li>Go to and click Share </li>
    <img src="https://i.imgur.com/EwMv8rK.png" width="600" alt="NFS"/>
  </ul>
</p>
<br />


<h2>Step 4: Give the "write-access" folder read/write permission level</h2>
<b>Allow the write-access folder read/write permissions for the domain users</b>
<ul>
  <li>Right click the folder > Select Properties</li>
  <li>Press the Sharing tab</li>
  <li>Click the Share button</li>
  <img src="https://i.imgur.com/S5sODpk.png" width="600" alt="NFS"/>
  <li>Type the Domain Users in the box</li>
  <li>Click the Add button</li>
  <li>Set the permission level for the Domain Users to Read/Write > Click Share</li>
  <img src="https://i.imgur.com/NBQn82T.png" width="600" alt="NFS"/>
  <img src="https://i.imgur.com/3aNVYC7.png" width="600" alt="NFS"/>
</ul>
<br />


<h2>Step 5: Give the "no-access" folder read/write permission level for Domain Admins ONLY</h2>
<b>Give the no-access folder read/write permission level for Domain Admins ONLY. No domain users wiil be allowed access to this file</b>
<ul>
  <li>Right click the folder > Select Properties</li>
  <li>Click the Sharing tab</li>
  <li>Click the Share button</li>
  <img src="https://i.imgur.com/2ghTGqg.png" width="600" alt="NFS"/>
  <li>Type the Domain Admins in the box</li>
  <li>Click the Add button</li>
  <img src="https://i.imgur.com/xUadTPe.png" width="600" alt="NFS"/>
  <li>Set the Permission level for the Domain Admins to Read/Write</li>
  <li>Click Share</li>
  <li>This folder can be only access to Domain Admins and not by Domain users</li>
  <img src="https://i.imgur.com/YeaeFEb.png" width="600" alt="NFS"/>
</ul>
<br />


<h2>Step 6: Log into CLIENT-1 as any user from Active Directory</h2>
<b>Choose any user from your Active Directory to log into our CLIENT-1 vm</b>
<img src="https://i.imgur.com/hLJf2Ls.png" width="600" alt="NFS"/>
<br />


<h2>Step 7: Try to Access the folders as the Domain User</h2>
<b>See if the Domain User has certain access to specific files</b>
<ul>
  <li>Go to File Explorer</li>
  <li>On the top bar, type \DC-1</li>
  <li>This will reference the files we created on DC-1.
</li>
  <img src="https://i.imgur.com/33bROV2.png" width="600" alt="NFS"/>
  <img src="https://i.imgur.com/PKL2MyM.png" width="600" alt="NFS"/>
  <li>Open write-access</li>
  <li>The Domain User should be able to read/write in this folder</li>
  <li>I created a document while logged in as the Domain User.
</li>
  <img src="https://i.imgur.com/HAqWzrU.png" width="600" alt="NFS"/>
  <li>Open read-access</li>
  <li>The Domain User should be able to see and read inside the folder</li>
   <img src="https://i.imgur.com/MQiXU1j.png" width="600" alt="NFS"/>
  <li>However, if the Domain User tries to create documents inside, they receive the following error message.
</li>
  <li>It states that they need permission to perform this action.
</li>
  <img src="" width="600" alt="NFS"/>
  <li>Open no-access</li>
  <li>Notice that the Domain User is unable to access the folder at all.
</li>
  <li>This is because the folder was configured to be accessible only by Domain Admins.
</li>
  <img src="https://i.imgur.com/00DtjXJ.png" width="600" alt="NFS"/>
</ul>
<br />


<h2>Step 8: Return to our DC-1 vm to create a Security Group</h2>
<b>We are going to assign our accounting folder to a Security Group</b>
<ul>
  <li>Open up Active Directory Users and Computers</li>
  <li>Right click on mydomain.com > New > Organizational Unit</li>
  <li>Name the Organizational Unit, _GROUPS</li>
  <img src="https://i.imgur.com/fK0GjWC.png" width="600" alt="NFS"/>
  <li>In the right panel, right click > Select New > Group</li>
  <li>Name the Group ACCOUNTANTS</li>
  <img src="https://i.imgur.com/giXDffA.png" width="600" alt="NFS"/>                                                       
</ul>
<br />


<h2>Step 9: Share the Accounts folder to the ACCOUNTANTS Security Group</h2>
<b>We are assigning the Accounts folder to the ACCOUNTANTS Security Group</b>
<ul>
  <li>Go to File Explorer and find the accounting folder</li>
  <li>Right click > Properties</li>
  <li>Go to the Sharing tab</li>
  <li>Click the Share button</li>
  <img src="https://i.imgur.com/jE9I183.png" width="600" alt="NFS"/> 
  <li>Add the Security Group, ACCOUNTANTS to the box</li>
  <li>Click the Add button</li>
  <li>Allow it the Permission level of Read/Write</li>
  <img src="https://i.imgur.com/FnCK3BZ.png" width="600" alt="NFS"/> 
</ul>
<br />


<h2>Step 10: Try to access the "accounting" folder as the Domain User</h2>
<b>Next, we’ll observe what happens when the Domain User attempts to access the Accounts folder</b>
<ul>
  <li>Go to the File Explorer and click on the Accounts folder in CLIENT-1 vm</li>
  <li>You will notice the user user don't have access to the folder</li>
  <li>This is because the user is not assigned to the Security Group named **ACCOUNTANTS**.
</li>
  <img src="https://i.imgur.com/YbbJGsk.png" width="600" alt="NFS"/> 
  <img src="https://i.imgur.com/vOyYDs9.png" width="600" alt="NFS"/> 
</ul>
<br />


<h2>Step 11: Assign the Domain User to the Security Group</h2>
<b>We will assign the Domain User to the Security Group called ACCOUNTANTS to allow access to the folder</b>
<ul>
  <li>Go back to Active Directory Users and Computers on DC-1</li>
  <li>Double click the ACCOUNTANTS Security group</li>
  <li>Go to the Members tab > Click add</li>
  <li>Add the user's name > Check names > Click OK</li>
  <img src="https://i.imgur.com/1dRDDcy.png" width="600" alt="NFS"/> 
  <img src="https://i.imgur.com/irEgtfn.png" width="600" alt="NFS"/> 
  <li>The User is now added to the Security Group</li>
</ul>
<br />


<h2>Step 12: Try to access the "accounting" folder again in CLIENT-1</h2>
<b>You might have to log out then on as the user to let the folder and Security Group update</b>
<ul>
  <li>Go to File Explorer and find the accounting folder and open it</li>
  <img src="https://i.imgur.com/7rSEFC0.png" width="600" alt="NFS"/> 
  <li>You should now be able to see the contents in this folder and edit them</li>
  <img src="https://i.imgur.com/uDuBHhU.png" width="600" alt="NFS"/> 
</ul>
<br />
