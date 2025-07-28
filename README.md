<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>🎟️ Setting Up osTicket on an Azure Windows VM</h1>
<p>This tutorial will guide you through setting up osTicket on a Windows 10 Azure Virtual Machine (VM), including installing IIS, PHP, MySQL, and the osTicket application.</p>

<h1>🧠 Overview</h1>

<p>You will be installing and configuring osTicket on a Windows 10 Virtual Machine in Microsoft Azure. Perfect for IT students, system administrators, and helpdesk engineers learning ticketing systems in the cloud.</p>

<h2>What You’ll Learn:</h2>

- How to deploy a Windows 10 VM in Azure
- How to install and configure IIS, PHP, MySQL, and osTicket
- How to manage roles, users, departments, SLAs, and more within osTicket
- How to use your local machine (macOS or Windows) to remote into your Azure VM

<h2>Environments and Technologies to use</h2>

- Microsoft Azure (Virtual Machines)
- Microsoft RD Client (Remote Desktop)
- Required Files to Use - [Download osTicket Setup Package](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

<h2>Operating Systems to use</h2>

- macOS Sonoma ***(if you own Macbook Air M1 or M2; it does not matter what type of macOS you own)***
- Windows 10 or Windows 11 Home or Pro ***(if you own either of them)***

-----

## 🧱 Part 1: Create the Azure Virtual Machine

1. Create a Resource Group & Virtual Network:
   - VM Name: `osticket-vm`
   - vCPUs: `4`
   - Username: (any easy username to remember)
   - Password: (any easy password to remember)

2. Log Into the VM
   - Use Remote Desktop to log into the VM (osticket-vm)
  
-----

## ⚙️ Part 2: Install osTicket and Components

<h2>📂 Step 1: Prepare Installation Files</h2>

1. Download `osTicket-Installation-Files.zip` from the link above.
2. Extract and rename the folder to `osTicket-Installation`
  
<h2>🌐 Step 2: Install IIS with CGI</h2>

1. Go to `Control Panel` > `Programs` > `Turn Windows Features on or off`
2. Enable:
     - `Internet Information Services (IIS)`
     - Under `Application Development Features` > check ✅ `CGI`

<h2>🐘 Step 3: Install PHP and Dependencies</h2>

1. From the `osTicket-Installation folder`, install:
      - `PHPManagerForIIS_V1.5.0.msi`
      - Then `rewrite_amd64_en-US.msi`
2. Create and unzip to `C:\PHP`:
      - `php-7.3.8-nts-Win32-VC15-x86.zip`
3. Install `MySQL`:
      - `mysql-5.5.62-win32.msi` → Select Typical Setup
	  • Configure with:
	  • Username: `root`
	  • Password: `root`

<h2>🔧 Step 4: Configure IIS with PHP</h2>

1. Open `IIS Manager` as Administrator
2. Use `PHP Manager` to register: `C:\PHP\php-cgi.exe`
3. Restart `IIS` (Stop and Start)

<h2>📦 Step 5: Install osTicket</h2>

1. From the `osTicket-Installation` folder:
       - Unzip `osTicket-v1.15.8.zip`
	  • Copy upload folder to: `C:\inetpub\wwwroot`
       - Rename it to `osTicket`
2. Restart `IIS` again
  
<h2>🧩 Step 6: Enable PHP Extensions</h2>

1. In IIS, go to `Sites` > `Default` > `osTicket`.
2. Click `PHP Manager`.
3. Enable the following extensions:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`
4. Refresh the osTicket site in your browser.

<h2>🛠️ Step 7: Configure osTicket Files</h2>

1. Rename config file: 
     - Path from: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
     - Rename to: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`.
***(Another word, remove the sample)***

2. Set file permissions:
    - Disable inheritance
    - Remove all permissions
    - Add `Everyone` → `Full Control`

<h2>🌐 Step 8: Complete Setup in Browser</h2>

1. Install `HeidiSQL` from the installation folder
2. Create a new session:
     • Username: `root`
     • Password: `root`
     • Create database: `osTicket`
3. Open a browser in the VM: `http://localhost/osTicket`
4. Enter:
     • Database: `osTicket`
     • MySQL Username: `root`
     • MySQL Password: `root`
     • Click: `Install Now`

<h2>🔐 Step 9: Secure Your Installation</h2>

1. Access:
      • Admin: `http://localhost/osTicket/scp/login.php`
      • End User: `http://localhost/osTicket/`
2. Delete the /setup folder
3. Set `ost-config.php` to `Read-only`

-----

## 🧭 Part 3: Post-Installation Setup

1. 👥 Configure Roles & Agents
    - Go to: `Admin Panel` → `Agents` → `Roles`
       • Add: `Supreme Admin`, `Support Staff`, etc.
       • Go to: `Agents` → `Add New`
       • Add agents like `Jane`, `John`, etc.

2. 🏢 Set Up Departments and Teams
     - Go to: `Agents` → `Departments` → `Add “System Administrators”`
     - Go to: `Agents` → `Teams` → `Add “Level I”` and `“Level II Support”`

3. 🧑‍💼 Allow Ticket Creation
     - Go to: `Settings` → `User Settings`
     - Set to: Require registration and login to create tickets
  
4. ⏱️ Configure SLAs
     - Go to: `Manage` → `SLA`
	• Sev-A: 1 hour, 24/7
	• Sev-B: 4 hours, 24/7
	• Sev-C: 8 hours, business hours

5. 📋 Help Topics
     - Go to: Manage → Help Topics → Add:
	• Business Critical Outage
	• Personal Computer Issues
	• Equipment Request
	• Password Reset
  
-----

### 🎫 Part 4: Practice Ticket Management

1. Create tickets as a user
2. Respond and resolve them as an agent
3. Triage based on severity level (Sev-A, B, C)
  
-----

## ✅ Final Thoughts

You’ve installed and configured osTicket in an Azure-hosted Windows environment! This helpdesk system is a great way for you to learn real-world ticket management and internal IT operations.

- 🔐 Next Steps (Optional)
	• Enable email piping with SMTP
	• Integrate LDAP authentication
	• Set up SSL with a self-signed certificate

-----

## 💡 Helpful Tips

- Use macOS or Windows with Microsoft Remote Desktop to connect
- Test with real scenarios (password resets, equipment requests, escalations)
- Backup your VM regularly in Azure for disaster recovery

-----

### 🧠 Want to Learn More?

- [osTicket Docs](https://docs.osticket.com/en/latest/)

- [Azure VM Setup](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)
