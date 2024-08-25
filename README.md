<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Installing and Configuring osTicket on Azure VM</h1>
<p>This tutorial guides you through setting up osTicket on a Windows 10 Virtual Machine (VM) in Azure. You'll create the VM, install necessary software, and configure osTicket for helpdesk management.</p>

<h2>Environments and Technologies to use</h2>

- Microsoft Azure (Virtual Machines)
- Microsoft RD Client (Remote Desktop)
- Installtion Links

<h2>Operating Systems to use</h2>

- macOS Sonoma ***(if you own Macbook Air M1 or M2; it does not matter what type of macOS you own)***
- Windows 10 or Windows 11 Home or Pro ***(if you own either of them)***

-----

Links:
osTicket Installation Files: https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

-----

## Part 1: Create the Virtual Machine

1. **Create a Resource Group**:
   - Start by creating a new Resource Group in Azure.

2. **Create a Windows 10 VM**:
   - Create a Windows 10 VM with 2-4 Virtual CPUs.
   - Allow the VM setup to create a new Virtual Network (VNet).
  
-----

## Part 2: Install osTicket

1. **Prepare the VM**:
   - **VM Name**: Vm-osticket
   - **Username**: labuser (or your choice)
   - **Password**: osTicketPassword1! (or your choice)

2. **Install Required Software**:
   - **IIS Setup**:
     - Open IIS Manager and install the following:
       - CGI and Common HTTP Features
       - IIS Management Console
      
![image](https://github.com/user-attachments/assets/9a35d051-2d12-4229-8c5a-4221d4efe295)

   - **Download and Install Software**:
     - PHP Manager for IIS: Download and install `PHPManagerForIIS_V1.5.0.msi`.
     - Rewrite Module: Download and install `rewrite_amd64_en-US.msi`.
     - PHP 7.3.8: Download `php-7.3.8-nts-Win32-VC15-x86.zip` and unzip it into `C:\PHP`.
     - VC_redist.x86.exe: Install this from the Installation Files.
     - MySQL 5.5.62: Install using `mysql-5.5.62-win32.msi` and set the password to `Password1`.
    
-----

***Note: If this appears, don't worry, you're not going to be infected. Choose to 'Keep' the file and open to download.***

![image](https://github.com/user-attachments/assets/b27aa563-139e-4b15-920e-c21d83405342)

![image](https://github.com/user-attachments/assets/5d905403-f71e-438a-804c-1c57dea35645)

-----

3. **Configure IIS**:
   - Open IIS Manager as an admin.
   - Register PHP in IIS and reload IIS by stopping and starting the server.

4. **Install osTicket**:
   - Download osTicket v1.15.8 from the Installation Files.
   - Extract and copy the “upload” folder to `C:\inetpub\wwwroot` and rename it to `osTicket`.
   - Reload IIS (stop and start the server).

5. **Configure osTicket**:
   - Visit `http://localhost/osTicket` and continue the setup.
   - Rename `ost-sampleconfig.php` to `ost-config.php` and assign permissions to "Everyone" with "All" access.
   - Set up osTicket through the web interface:
     - **MySQL Database**: osTicket
     - **MySQL Username**: root
     - **MySQL Password**: Password1

6. **Complete Installation**:
   - Browse to the helpdesk login page: `http://localhost/osTicket/scp/login.php`.
   - Clean up by deleting `C:\inetpub\wwwroot\osTicket\setup` and setting `ost-config.php` to "Read" only.
  
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

By following these steps, you have successfully installed and configured osTicket on your Azure VM. You’ve set up a helpdesk system capable of managing tickets, configured roles and departments, and ensured that your system is ready for use. Congratulations on completing the setup!
