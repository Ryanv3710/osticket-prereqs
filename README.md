<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
</br>
<h2>Links:</h2>
<p>osTicket installation files:</p>
<a href="https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Installation files</a>
<h2>Descriptive outline of the steps required for successful osTicket setup</h2>

1. Create the Resoure Group in Azure
  <ul>
  <li>On the main page of Azure you will see a heading called "Azure Services" just below that you will see "Resource Groups" click that option. Or in the search bar you can manually type it in.</li>
  <li>Now we create our Resource Group and name it. </li>
  <ul>
        <li>Resource Group: RG-osTicket</li>
      <li>Region: (US) East US (Just ensure you take note of the region you use.)</li>
      <li>Click "Review + Create" and create the resource.</li>
      
      
  </ul>
    </ul>
 
  </br>
  2. Create Virtual Machine in Azure
<ul>
  <li>To create the virtual machine, in the search bar type in "virtual machines" </li>
  <li>You'll see "No virtual machines to display" just below that it'll say "create" click that option and click azure virtual machine.</li>
  <ul>
    <li>Resource Group: RG-osTicket (place in orginial RG, we're not creating another RG)</li>
      <li>Virtual machine name: vm-osTicket</li>
      <li>Region: (US) East US</li>
      <li>Zone: keep in Zones 1</li>
      <li>Image: Windwos 10 Pro, version 21H2 - x64 Gen2</li>
    <li>2-4 Virtual CPUs</li>
      <li>Username: labuser (just an example, you can create your own)</li>
      <li>Password: Password1 (can create your own, just take note of your user/pass etc. in your notepad)</li>
  </ul>
  <li>The virtual network will be automatically created but you can check just in case, now just review + create.</li>
  <li>Navigate to "Network Watcher" by typing in search bar & observe the topology with the resources you created (vnet,nsg,ip etc.)</li>
  <ul>
    <li>Note: if it says "No network watcher present in this subscription" on left side of the navigational list click "Overview" & move resource group from network watcher to RG-osTicket.</li>
  </ul>
  
  </ul>
  </br>
  
  3. RDP to Windows Server & install files (pre-install)

  <ul>
  <li>Open: <a href="https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Installation files</a></li>
  - These are the files needed to install osTicket, so copy and paste this url into your windows VM to save you time of moving back and forth.
  
  


  <li>Install / Enable IIS in Windows <u>WITH CGI</u></li>
  - Control panel -> programs -> turn windows features on or off -> IIS -> World Wide Web Services -> Application Development features -> [x] CGI

  <li>From installation Files downnload and install <a href="https://drive.google.com/file/d/1RHsNd4eWIOwaNpj3JW4vzzmzNUH86wY_/view?usp=share_link"> PHP Manager for IIS</a></li>
  <li>From installation Files, download and install the <a href="https://drive.google.com/file/d/1tIK9GZBKj1JyUP87eewxgdNqn9pZmVmY/view?usp=share_link">Rewrite Module</a></li>
  - Create the directory C:\PHP in folders
  <li>From the installation Files, download <a href="https://drive.google.com/file/d/1snNMtLdCOpMtkCyD4mvl9yOOmvVIp9fP/view?usp=share_link">PHP 7.3.8</a></li>
  - unzip contents into C:\PHP 
  <li>From the Installation Files, download and install <a href="https://drive.google.com/file/d/1s1OsGF3-ioO0_9LYizPRiVuIkb3lFJgH/view?usp=share_link">VC redist.x86.exe</a></li>
  <li>From the Installation Files, download and install <a href="https://drive.google.com/file/d/1_OWh9p7VQLcrB0q_V7qT8yHl0xo5gv7z/view?usp=share_link">MySQL 5.5.62</a></li>
  - Typical Setup
  - Launch Configuration Wizard (after install)
  - Standard Configuration
  '- Password1
    <li>Open IIS as an Admin</li>
    <li>Register PHP from within IIS</li>
    <li>Reload IIS (Open IIS, stop and start the server)</li>
    <li>Install osTicket v1.15.8</li>
  - Download osTicket from the Installation Files Folder
  - Extract and copy "upload" folder to c:\inetpub\wwwroot
  - Within c:\intepub\wwwroot, Rename "upload" to "osTicket"
    <li>Reload IIS (Open IIS, stop and start the server)</li>
    <li>Go to sites -> Default -> osTicket</li>
  - On the right, click "Browse *.80"

  <li>Enable the extensions below</li>
  <ul>
    <li>Go back to IIS, sites -> Default -> osTicket</li>
    <li>Double-click PHP Manager</li>
    <li>Click "Enable or disable an extension"</li>
    <li> Enable: php_imap.dll</li>
    <li>Enable: php_intll.dll</li>
    <li>Enable: php_opache.dll</li>
    <li>Refresh the osTicket and observe the changes</li>
  </ul>
  <li>Rename: ost-config.php</li>
  <ul>
    <li>From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php</li>
    <li>To: C:\inetpub\wwwroot\osTicket\include\ost-config.php</li>
  </ul>
  <li>Assign Permissions: ost-config.php</li>
  <ul>
    <li>Disable inheritance -> Remove All
</li>
      <li>New Permissions -> Everyone -> All
</li>
  </ul>
  <li>Continue Setting up osTicket in the browser (click continue)</li>
  <ul>
    <li>Name Helpdesk</li>
     <li>Default email (receives email from customers)</li>
  </ul>
  <li>From the installation Files, download and install <a href="https://docs.google.com/document/d/1WovrX2DaS9xkfaSr4LXyB4YnnWpXIgPCMMbbfgHmGVw/edit">HeidiSQL</a></li>
  <ul>
    <li>open Heidi SQL</li>
        <li>Create a new session, root/Password1</li>
        <li>Connect to the session</li>
        <li>Create a database called "osTicket"</li>
  </ul>

  <li>Congratulations, hopefully it is installed with no errors</li>
  <ul>
    <li>Browse to your help desk login page: <a href="http://localhost/osTicket/scp/login.php">http://localhost/osTicket/scp/login.php</a></li>
  </ul>
  <li>End Users osTicket URL:</li>
  <ul>
    <a href="http://localhost/osTicket/">http://localhost/osTicket/</a>
  </ul>
  <li>Clean up</li>
  <ul>
    <li>Delete: C:\inetpub\wwwroot\osTicket\setup
</li>
    <li>Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php
</li>
  </ul>
  <li>Notes:</li>
    <ul>
      <li>Browse to your help desk login page: <a href="http://localhost/osTicket/scp/login.php">http://localhost/osTicket/scp/login.php</a>/li>
      <li>End Users osTicket URL: <a href="http://localhost/osTicket/">http://localhost/osTicket/</a>
  </ul>
  </ul>

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
