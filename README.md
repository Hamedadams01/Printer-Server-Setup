# Printer Server

## Overview

In this lab, I installed and configured the Print and Document Services role on a Windows Server 2019 domain controller (Houtech), turning it into a centralized print server. This involved adding the role and its management tools, creating a new shared printer using a built-in driver, publishing it to Active Directory, locking down access to the HR department's security group, and finally testing the full setup from the perspective of an HR end user on a Windows 11 client.

## Objectives


- Install the Print and Document Services role, including the Print Server role service and management tools
- Review the Print Management console and existing default printers before adding a new one
- Create a new printer using the Network Printer Installation Wizard with a built-in Windows driver
- Share the printer and publish it to Active Directory for discoverability
- Remove default "Everyone" access and grant printing rights to the HR security group specifically
- Verify the printer is discoverable through an AD printer search
- Test the full setup end-to-end by signing in as an HR test user and adding the printer on a client


## Descriptions

1 — Reviewing prerequisites before installing the role

Opened Server Manager on Houtech and launched the Add Roles and Features Wizard, reviewing the prerequisites on the "Before You Begin" screen (strong Administrator password, static network settings, current security updates) before beginning the Print and Document Services role installation.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045127.png?raw=true)

2 — Adding required management tools

When selecting the Print and Document Services role, Windows prompted to add the required management tools, including Print and Document Services Tools under Role Administration Tools. Kept "Include management tools (if applicable)" checked and clicked Add Features to ensure the Print Management console would be available after installation.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045150.png?raw=true)

3 — Selecting the server role

On the Select server roles screen, checked Print and Document Services, which the description confirmed would centralize print server and network printer management tasks, committing to installing the role on Houtech.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045155.png?raw=true)

4 — Selecting the role service

On the Select role services screen, checked Print Server, which the description explained includes the Print Management snap-in used for managing multiple printers or print servers and migrating printers between Windows print servers, rather than the Internet Printing or LPD Service options.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045222.png?raw=true)

5 — Opening Print Management

After the installation finished, confirmed the Print Services dashboard in Server Manager showed HOUTECH online, then opened the Tools menu and selected Print Management to access the console used to add and manage printers.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045421.png?raw=true)

6 — Reviewing existing default printers

Inside Print Management, expanded Print Servers > Houtech (local) > Printers and saw the two default printers already present, Microsoft Print to PDF and Microsoft XPS Document Writer, both showing a Ready queue status, before adding a new shared printer.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045538.png?raw=true)

7 — Launching the Add Printer wizard

Right-clicked the Printers node, which opened a context menu with options including Add Printer, Show Extended View, Refresh, and Export List, and selected Add Printer to launch the Network Printer Installation Wizard.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045710.png?raw=true)

8 — Choosing the printer port

In the Network Printer Installation Wizard, selected "Add a new printer using an existing port" and left it set to LPT1: (Printer Port), since this was a virtual/test printer for the lab rather than a physical network printer connected by IP address.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045732.png?raw=true)

9 — Choosing to install a new driver

On the Printer Driver screen, selected "Install a new driver" instead of using an existing driver on the computer, to pick a specific driver for the new printer rather than reusing one already installed.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20045749.png?raw=true)

10 — Selecting the printer driver

Selected "Microsoft MS-XPS Class Driver 2" from the list of available Microsoft printer drivers, using a built-in, digitally signed Windows driver for the lab printer instead of needing to source a physical printer's driver files.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050302.png?raw=true)

11 — Naming and sharing the printer

On the Printer Name and Sharing Settings screen, confirmed the printer name as "Microsoft MS-XPS Class Driver 2" and reviewed the "Share this printer" option before finishing the wizard, setting a clear, identifiable name before configuring sharing separately in its properties.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050329.png?raw=true)

12 — New printer created

Back in Print Management, saw the new Microsoft MS-XPS Class Driver 2 printer listed with a Ready queue status, 0 jobs in queue, and Houtech (local) as the server name, verifying the printer was successfully created before configuring sharing and permissions.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050444.png?raw=true)

13 — Reviewing printer properties

Opened the new printer's Properties dialog and reviewed the General tab, which showed its model and features (Color: No, Double-sided: No, Staple: No, Maximum resolution: 300 dpi) along with Letter as the available paper size, confirming its basic configuration before sharing it out to the network.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050510.png?raw=true)

14 — Publishing the printer to Active Directory
Checked "List in the directory" on the Sharing tab so the printer would be published in Active Directory, making it discoverable by users searching for printers through AD rather than requiring them to know the exact server and share name.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050608.png?raw=true)

15 — Confirming the sharing settings

Reviewed the full Sharing tab dialog again, confirming "Share this printer," "Render print jobs on client computers," and "List in the directory" were all checked, finalizing the printer's sharing configuration.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051530.png?raw=true)

16 — Verifying the printer port

On the Ports tab, confirmed the printer was using LPT1: (Printer Port), with other available ports (LPT2, LPT3, and several COM ports) listed but unchecked, verifying it was bound to the correct port before locking down who could use it.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050638.png?raw=true)

17 — Removing default access

On the Security tab, selected the default "Everyone" group and clicked Remove, taking away the printer's default wide-open access since printing rights needed to be restricted to a specific department rather than every domain user.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20050739.png?raw=true)

18 — Adding the HR security group

Clicked Add and typed "#Human_Resources" into the object name field of the Select User, Computer, Service Account, or Group dialog, granting printer access specifically to the HR department's existing security group instead of adding individual users.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051048.png?raw=true)

19 — Verifying the permission entry

Opened Advanced Security Settings for the printer and confirmed #Human_Resources now appeared in the permission entries list with Print access allowed, double-checking the permission was applied correctly at a granular level.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051116.png?raw=true)

20 — Confirming HR print access

Back on the Security tab, selected #Human_Resources in the group list and confirmed the Print permission was set to Allow, as a final check that HR department users would be able to print once the printer was deployed to their machines.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051128.png?raw=true)

21 — Navigating to Control Panel

Navigated back out to the server's Control Panel main screen, moving from printer configuration work over to verifying the printer's presence in the server's Devices and Printers view.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051316.png?raw=true)

22 — Verifying the printer in Devices and Printers

In Devices and Printers, confirmed the Microsoft MS-XPS Class Driver 2 printer appeared under Printers (3) with a green checkmark indicating it was set as the default, alongside Microsoft Print to PDF and Microsoft XPS Document Writer, showing 0 documents in queue, verifying it was fully registered and idle on the server side.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051325.png?raw=true)

23 — Opening Find Printers in Active Directory

From Active Directory Users and Computers, opened the Find Printers dialog, set the search scope to Houtech.local, and left the Name, Location, and Model fields blank before clicking Find Now, to confirm the printer published earlier could actually be located through an AD search.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051641.png?raw=true)

24 — Confirming the printer is discoverable

The search returned one result, the Microsoft MS-XPS Class Driver 2 printer, confirming "1 item(s) found," proving that checking "List in the directory" earlier had actually worked and the printer was discoverable through Active Directory.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20051719.png?raw=true)

25 — Verifying the HR test user's group membership

Opened Emily Garcia's user properties and checked the Member Of tab, confirming she belonged to both #Human_Resources (Houtech.local/Department/Human Resources(HR)) and the default Domain Users group, confirming she was a valid HR department test user before using her account to test client-side printer access.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052125.png?raw=true)

26 — Signing in as the HR test user

On the Windows 11 client, signed in as Emily Garcia (egarcia@Houtech.local) to test the printer setup from the perspective of an actual HR department end user, rather than testing everything as a domain administrator.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052151.png?raw=true)

27 — Reviewing existing printer preferences

Opened Settings > Bluetooth & devices > Printers & scanners on the client and reviewed the existing printer preferences, including "Let Windows manage my default printer," which was turned on, to see the client's starting printer configuration before adding the new network printer.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052535.png?raw=true)

28 — Discovering the shared printer

Clicked "Add a printer or scanner," and Windows automatically discovered "Microsoft MS-XPS Class Driver 2 on HOUTECH" as an available network printer, confirming the client could see the printer shared and published from the server without any manual path entry.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052554.png?raw=true)

29 — Connecting to the printer
Clicked Add device, and the printer's status changed to "Connecting," beginning the actual connection process between the client and the shared network printer.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052602.png?raw=true)

30 — Confirming successful installation

Windows confirmed "You've successfully added Microsoft MS-XPS Class Driver 2 on Houtech.Houtech.local," noting the printer was installed with the Microsoft enhanced Point and Print driver, verifying the driver installed correctly on the client without errors.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052711.png?raw=true)

31 — Option to print a test page

On the final wizard screen, was given the option to print a test page before clicking Finish, as the ultimate proof that the printer was fully functional end to end, from server-side sharing and permissions all the way through to a working client connection.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052719.png?raw=true)

32 — Final verification on the client
Opened the printer's settings page one more time and confirmed its status showed Idle, with options available to open the print queue, print a test page, view printer properties, and adjust printing preferences, confirming the printer was fully installed, connected, and ready for Emily Garcia to use for day-to-day printing.

![image alt](https://github.com/Hamedadams01/Printer-Server-Setup/blob/main/Screenshot%202026-06-28%20052739.png?raw=true)
