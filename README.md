<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Pre-Installation</h1>
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
  
  3. RDP to Windows Server & install files 

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
      <li>End Users osTicket URL: <a href="http://localhost/osTicket/">http://localhost/osTicket/</a></li>
  </ul>
  </ul>

<h2>Visual demonstration of Pre-Installation</h2>
</br>

<h3>1. Create the Resoure Group in Azure</h3>
<p>
<img src="https://i.imgur.com/sxb9slz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the main menu you'll see "azure services" click resource group. Now is where we will name our resource group & select the region, you want it in the region you are in based on your vicinity but if you choose another one just make sure you take note of not only the region but the name of your resource group in your notepad notes.
</p>
<br />

<h3>2. Create Virtual Machine in Azure</h3>
<p>
<img src="https://i.imgur.com/mnEv5lc.png" height="100%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Your resource group may take time to load but you will be notified when it successfully got created. Meanwhile, you can still create your virtual machine in windows while you wait. To create the virtual machine go to the search bar and type "virtual machine" or in the web browser you can copy and paste this "https://portal.azure.com" which will take you back to the main menu. 
</p>

<img src="https://i.imgur.com/cfQ3dXw.png" height="100%" width="80%" alt="Disk Sanitization Steps"/>
<p>
  Now, put your virtual machine in the resource you created. In my case (RG-osTicket) then name your VM & ensure it is in the same region as your resource group. Also you will create the VM in windows 10, make sure it has 2-4 vcpu's. Finally, create your username/password and agree to the terms.
  </p>
<br />
<img src="https://i.imgur.com/hBqKWO0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
  Review information & then create the VM
  </p>
<p>
  
  </br>
  
  <h3>3. RDP to Windows Server & install files</h3>
  <p>
  
<img src="https://i.imgur.com/i2nPzxM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to your VM machine & locate the public IP address and copy it. This is the IP address you will use to remotely connect to the windows machine. To do so, in your task bar search bar type in "renmote desktop connection" click it and then take the copied IP address & paste it into the RDC. Remember the username and password you created when creating the vM? those are the credentials you'll use to log into the VM.
</p>

<p>
<img src="https://i.imgur.com/z57neVz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  We need to enable CGI so to do so,  Control panel -> programs -> turn windows features on or off -> IIS -> World Wide Web Services -> Application Development features -> [x] CGI. in a separate window if you type the ip '127.0.0.1' it should load a blue page with icons but at the top it says Internet Information Services.

  </p>

<p>
<img src="https://i.imgur.com/PUAVeIq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
 
Now we can start to download the files from the Installation Folder & be able to maneuver to different directories or create directories. First, we are going to download and install "PHP Manager for IIS" do not make any changes to installion setup just click next & agree to the terms. 
  </p>
  

<img src="https://i.imgur.com/4jzPw4T.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>



<p>
 Next from the installation folder we are going to download and install the "Rewrite Module"

  </p>
  

<img src="https://i.imgur.com/1CikBSA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<p>
 Going back to the Installation Folder locate "PHP 7.3.8" download the file. As that is downloading go to your C drive in your folder and create a folder called "C:\PHP" Once the file downloads we are going to unzip or extract all the contents in the PHP 7.3.8 into the C:\PHP folder. 

  </p>
  
  <p>
  NOTE: if when the file downloads and gives you a trust error, in the downloads locate the file and click the 3 dots next to it to which it will have an option "keep" click keep and then click "keep anyway" after which will allow you to continue with unzipping the file.
  </p>
  
   
<p>
<img src="https://i.imgur.com/1CikBSA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
 Going back to the Installation Folder locate "PHP 7.3.8" download the file. As that is downloading go to your C drive in your folder and create a folder called "C:\PHP" Once the file downloads we are going to unzip or extract all the contents in the PHP 7.3.8 into the C:\PHP folder. 

  </p>
  <p>
  <img src="https://i.imgur.com/njykJeJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
In the Installation Files locate VC redist.x86.exe. and download and install the file.
  </p>
  
 
  <img src="https://i.imgur.com/QzE83dK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<p>
From Installation Folder locate,download,and install MySQL 5.5.62
  <ul>
    <li>Typical setup</li>
    <li>Launch Configuration Wizard (after install)</li>
    <li>Standard configuration </li>
    <li>Password1 (create a password but take note)</li>
    </ul>

  </p>
  
  
  <p>
<img src="https://i.imgur.com/uzvopTh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open IIS as an admin & go back to the installation folder to download Install osTicket v1.15.8. Once it downloads copy and paste the "upload" folder within c:\inetpub\wwwroot, and rename the upload folder to "osTicket" Then you'll go to Go to sites -> Default -> osTicket. On the right click browse *.80
</p>

<p>
  Go back to IIS, sites -> Default -> osTicket, double click PHP Manager and enable these extensions.
  </p>
  
  <ul>
  <li>php_imap.dll</li>
    <li>php_intl.dll</li>
    <li> php_opcache.dll</li>
    <li>Refresh the osticket in your browser and observe the changes</li>
  </ul>
  
  
   <p>
<img src="https://i.imgur.com/Y0wzmPN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to installation Folder & install Heidi SQL. Create a new session and connect to the session & create a database called osTicket. Go back to osTicket in browser and apply the database,user,pass to the required fields and then continue and bam! you have successfuly installed osTicket 👍 All thats left is to go back to C:\inetpub\wwwroot\osTicket\setup & delete setup. After that configure the os-config.php to read only.
</p>
  
