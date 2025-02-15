<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Installing and Configuring osTicket on Azure VM</h1>
<p>This tutorial will guide you through setting up osTicket on a Windows 10 Azure Virtual Machine (VM), including installing IIS, PHP, MySQL, and the osTicket application.</p>

<h2>Environments and Technologies to use</h2>

- Microsoft Azure (Virtual Machines)
- Microsoft RD Client (Remote Desktop)
- Installtion Links

<h2>Operating Systems to use</h2>

- macOS Sonoma ***(if you own Macbook Air M1 or M2; it does not matter what type of macOS you own)***
- Windows 10 or Windows 11 Home or Pro ***(if you own either of them)***

-----

## Part 1: Create the Virtual Machine

1. **Create a Resource Group & Virtual Network**:
   - VM Name: osticket-vm
   - vCPUs: 4
   - Username: labuser
   - Password: osTicketPassword1!

2. **Log Into the VM**
   - Use Remote Desktop to log into the VM (osticket-vm)
  
-----

## Part 2: osTicket Installation Files

3. **Prepare osTicket Installation Files**
   - Download 'osTicket-Installation-Files.zip' to the desktop.
   - Unzip the folder and rename it to “osTicket-Installation-Files”.
  
4. **Install IIS with CGI**
   - Open Control Panel
   - Turn on Windows On or Off (which is the Windows Features).
   - Navigate to World Wide Web Services > Application Development Features.
   - Check CGI.
  
5. **Install PHP and Dependencies**
   - From the “osTicket-Installation-Files” folder:
	   •	Install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi).
	   •	Install the Rewrite Module (rewrite_amd64_en-US.msi).
   - Create a folder at C:\PHP.
      • Unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into C:\PHP.
      • Install VC_redist.x86.exe.
      • Install MySQL 5.5.62 (mysql-5.5.62-win32.msi).
         •	Select Typical Setup.
	      •	After installation, choose Standard Configuration.
	      •	Set Username: root and Password: root.
     
6. **Configure IIS and PHP**
   - 	Open IIS as Administrator.
   - Register PHP: In PHP Manager, add the PHP executable: C:\PHP\php-cgi.exe.
   - Reload IIS: Stop and Start the server.

7. **Install osTicket**
   - 	From the “osTicket-Installation-Files” folder:
	   •	Unzip osTicket-v1.15.8.zip.
	   •	Copy the upload folder to C:\inetpub\wwwroot.
	   •	Rename the folder from upload to osTicket.
   - Reload IIS (Stop and Start the server).
  
8. **Enable PHP Extensions**
   - In IIS, go to Sites > Default > osTicket.
   - Click PHP Manager.
   - Enable the following extensions:
      •	php_imap.dll
   	•	php_intl.dll
	   •	php_opcache.dll
   - Refresh the osTicket site in your browser.

9. **Configure osTicket**
   - Rename ost-sampleconfig.php to ost-config.php:
      •	Path: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
   	•	Rename to: C:\inetpub\wwwroot\osTicket\include\ost-config.php.
   - Set Permissions on ost-config.php:
      •	Disable inheritance and remove all permissions.
   	•	Add Everyone with Full Control.

10. **Complete osTicket Setup in Browser**
   - Install HeidiSQL from the “osTicket-Installation-Files” folder.
   - Open HeidiSQL and create a new session:
      •	Username: root
   	•	Password: root
   - Connect to the session and create a database named osTicket.

11. **Complete osTicket Setup in Browser**
   - Continue setting up osTicket in the browser:
      •	MySQL Database: osTicket
	   •	MySQL Username: root
	   •	MySQL Password: root
   - Click Install Now!.

12. **Access osTicket**
   - Helpdesk Login Page: http://localhost/osTicket/scp/login.php
   - End User URL: http://localhost/osTicket/

13. **Cleanup**
   - Delete the setup folder from C:\inetpub\wwwroot\osTicket.
   - Set Permissions on ost-config.php to Read only.

-----

## Part 3: Post-Installation Setup

1. **Configure Roles**:
   - Go to Admin Panel -> Agents -> Roles
   - Add roles such as Supreme Admin.

2. **Configure Departments**:
   - Go to Admin Panel -> Agents -> Departments
   - Add departments like System Administrators.

3. **Configure Teams**:
   - Go to Admin Panel -> Agents -> Teams
   - Add teams for Level I and Level II Support.

4. **Allow Ticket Creation**:
   - Go to Admin Panel -> Settings -> User Settings
   - Set registration to "Require registration and login to create tickets."

5. **Add Agents**:
   - Go to Admin Panel -> Agents -> Add New
   - Add agents like Jane and John.

6. **Add Users**:
   - Go to Agent Panel -> Users -> Add New
   - Add users like Karen and Ken.

7. **Configure SLA**:
   - Go to Admin Panel -> Manage -> SLA
   - Set SLAs for Sev-A (1 hour, 24/7), Sev-B (4 hours, 24/7), and Sev-C (8 hours, business hours).

8. **Set Up Help Topics**:
   - Go to Admin Panel -> Manage -> Help Topics
   - Add topics such as Business Critical Outage, Personal Computer Issues, Equipment Request, and Password Reset.
  
-----

## Part 4: Manage Tickets

1. **Practice Ticket Management**:
   - Create, triage, and resolve tickets.
   - For practice, refer to different ticket severity levels (e.g., Sev-A for major issues, Sev-B for moderate issues).
  
-----

## Conclusion

Congratulations, you’ve set up a helpdesk system capable of managing tickets, configured roles and departments, and ensured that your system is ready for use.
