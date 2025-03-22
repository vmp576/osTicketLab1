<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket - Prerequisites and Installation (Lab 1)

This project is the installation of osTicket. It starts from the “Basic” installation of a virtual machine conducted via the “Installing Virtual Machines in VMware” lab.

## Environments and Technologies Used

- “Basic” Virtual Machine in VMware
- [Exercise Files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

## Operating Systems Used
 - Windows 10 (22H2)

## Project Walk-Through
Begin with a “Basic” Virtual machine in VMware, either through snapshots or configuration. Then, we will be enabling IIS (Internet Information Services) with CGI.

- Open up the control panel
- Type "turn on Windows features" in the search box and click the "Turn Windows features on or off" link
- **Check and Expand** "Internet Information Services > Expand "World Wide Web Services" > Expand "Application Development Features" > And **Click to Enable CGI**

<img src="https://i.imgur.com/LUO762O.png" height="70%" width="70%"/>

You can verify that IIS has been installed properly by entering the loopback address (127.0.0.1) in Microsoft Edge.

<img src="https://i.imgur.com/FzQwm1Q.png" height="70%" width="70%"/>

Now, you will need to copy the exercise files into the Virtual Machine. There are two ways to do this. If you already downloaded the zip file, simply extract the osTicket Installation Files folder and copy it into your clipboard. Then, you can simply paste the folder into the virtual machine's desktop because bidirectional clipboard sharing is enabled by default.

Otherwise, go to the exercise files link inside the virtual machine and download it.

<img src="https://i.imgur.com/8ZAZk8G.png" height="70%" width="70%"/>

From the osTicket Installation Files folder, install PHP Manager for IIS.

<img src="https://i.imgur.com/pReGLOB.png" height="70%" width="70%"/>

After installing the PHP manager, install the Rewrite Module (rewrite_amd64_en-US)

<img src="https://i.imgur.com/8N4kqmM.png" height="70%" width="70%"/>

Then, create the C:\PHP folder.

<img src="https://i.imgur.com/F1RNfHf.png" height="70%" width="70%"/>

Unzip the php-7.3.8-nts-Win32-VC15-x86 zip file into the newly created PHP folder.

<img src="https://i.imgur.com/oIJ9GDc.png" height="70%" width="70%"/>

From the osTicket folder, install the VC_redist.x86.exe file. If the setup fails because another version of the product is already installed, then that is fine.

<img src="https://i.imgur.com/qcQuvgo.png" height="70%" width="70%"/>

Now, install the MySQL file using the following parameters and execute.

- Typical Setup ->
- Launch Configuration Wizard (after install) ->
- Standard Configuration ->
- **Modify Security Settings Root Password: root**

<img src="https://i.imgur.com/XXVEou1.png" height="70%" width="70%"/>

Run IIS as Administrator

<img src="https://i.imgur.com/XzTCCSe.png" height="70%" width="70%"/>

Double-click on PHP Manager > Register new PHP Version > Select the php-cgi.exe within the C:\PHP folder

<img src="https://i.imgur.com/E4NVsBI.png" height="70%" width="70%"/>

Select the IIS server (In my case, its name is DESKTOP-TSE6NGL), then restart the server by pressing stop and start

<img src="https://i.imgur.com/dZJ2KL9.png" height="70%" width="70%"/>

Back inside the osTicket installation files folder, **copy the upload folder** of the osTicket zip file into the c:\inetpub\wwwroot folder. Then, **rename the upload folder into osTicket.** After that, **reload the IIS server.**

<img src="https://i.imgur.com/SLST1pm.png" height="70%" width="70%"/>

In IIS, go from the server > sites > Default Web Site > osTicket > Browse *:80. If prompted to open the website with Edge, do so. The osTicket setup installer page should open.

<img src="https://i.imgur.com/cqnOWaa.png" height="70%" width="70%"/>

On the osTicket installation setup page, you will notice that some features are disabled**.** Go back into IIS > Sites > Default Web Site > osTicket > PHP Manager

Click “Enable or disable an extension and enable the following extensions:

- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opcache.dll

<img src="https://i.imgur.com/R8n6sjq.png" height="70%" width="70%"/>

Refresh the osTicket site and notice that some extensions are now enabled

<img src="https://i.imgur.com/tj8MpGp.png" height="70%" width="70%"/>

Enter the C:\inetpub\wwwroot\osTicket\include folder. Rename C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php

<img src="https://i.imgur.com/DgAlMMA.png" height="70%" width="70%"/>

Right-click the ost-config file > Properties > Security > Advanced >Change Permissions > **Disable Inheritance > Remove all inherited permissions**

<img src="https://i.imgur.com/CxGPfXz.png" height="70%" width="70%"/>

Modify the permissions. Go to Add > Principal > Type: everyone > Check Names > Full Control > OK > OK > Apply > OK

<img src="https://i.imgur.com/GnSXn0D.png" height="70%" width="70%"/>

From the osTicket installation files, install HeidiSQL. Keep clicking on Next and Install. Make sure that the settings to open HeidiSQL are enabled.

<img src="https://i.imgur.com/4nVc5VE.png" height="70%" width="70%"/>

Click on New and enter “root” in the user and password, then click on Open

<img src="https://i.imgur.com/tum7qZL.png" height="70%" width="70%"/>

Right-click the Unnamed database > Create New > Database > Name: **“osTicket” (Must Be Exact)**

<img src="https://i.imgur.com/8mLUKks.png" height="70%" width="70%"/>

Now, Continue the osTicket Installer setup. Configure the Basic Installation with the following parameters:

- Helpdesk Name: Helpdesk
- Default Email: helpdesk@helper.com
- Admin User First Name: Admin
- Admin User Last Name: User
- Admin User Email: adminuser@helper.com
- Admin Username: adminuser
- Admin Password: Password123!
- MySQL Database: osTicket
- MySQL Username: Root
- MySQL Password: Root

<img src="https://i.imgur.com/DJhDKR5.png" height="70%" width="70%"/>

Finally, to clean up the installation, delete the C:\inetpub\wwwroot\osTicket\setup folder and set the C:\inetpub\wwwroot\osTicket\include\ost-config.php to Read Only.

After completing everything, you can take a snapshot after completing osTicket (Lab 1). This is useful if you want to complete the following osTicket labs without redoing all the configuration.
