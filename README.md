# Printer-Server-Setup

# Overview
This project covers installing and configuring the Print and Document Services role on a Windows Server domain controller, then sharing and securing a printer for a specific department.
# Objectives

- Install the Print and Document Services role
- Configure a new printer through Print Management
- Share the printer and publish it to Active Directory
- Restrict access to a specific department group
- Verify the printer works end-to-end from a client machine

# Step-by-Step

- I opened Server Manager on Houtech and launched the Add Roles and Features Wizard, reviewing the "Before You Begin" prerequisites (strong Administrator password, static IP, current updates).
- I selected Print and Document Services on the Select server roles screen and kept "Include management tools (if applicable)" checked when prompted to add the Print and Document Services Tools.
- I confirmed the role description, which explained it would centralize print server and network printer management tasks.
- I selected Print Server on the Select role services screen (rather than Internet Printing or LPD Service), since I only needed the Print Management console.
- After installation, I confirmed HOUTECH showed Online in the Print Services dashboard, then opened Tools > Print Management.
- I expanded Print Servers > Houtech (local) > Printers and reviewed the two default printers (Microsoft Print to PDF, Microsoft XPS Document Writer) already in a Ready state.
- I right-clicked the Printers node and selected Add Printer to launch the Network Printer Installation Wizard.
- I selected "Add a new printer using an existing port" and left it on LPT1, since this was a virtual/test printer rather than a physical network device.
- I selected "Install a new driver" instead of reusing an existing one, then chose "Microsoft MS-XPS Class Driver 2" — a built-in, digitally signed Windows driver.
- I confirmed the printer name on the Printer Name and Sharing Settings screen before finishing the wizard.
- Back in Print Management, I confirmed the new printer showed a Ready status with 0 jobs in queue.
- I opened the printer's Properties and reviewed the General tab (Color: No, Double-sided: No, Max resolution: 300 dpi, Paper: Letter) to confirm its base configuration.
- On the Sharing tab, I checked "List in the directory" so the printer would be published in Active Directory and discoverable by name rather than requiring users to know the exact server/share path.
- On the Ports tab, I confirmed the printer was correctly bound to LPT1 before locking down permissions.
- On the Security tab, I selected the default "Everyone" group and clicked Remove to eliminate open access.
- I clicked Add and typed "#Human_Resources" into the object name field to grant access to the HR department's existing security group instead of individual users.
- I opened Advanced Security Settings and confirmed #Human_Resources appeared in the permission entries list with Print access allowed.
- I went back to the Security tab and confirmed the Print permission was set to Allow for #Human_Resources as a final check.
- I opened Devices and Printers on the server and confirmed the printer appeared under Printers (3), set as default with 0 documents in queue.
- I opened Active Directory Users and Computers, launched Find Printers, scoped to Houtech.local, and clicked Find Now with all fields blank.
- The search returned "1 item(s) found," confirming the printer was successfully published and discoverable in AD.
- I opened a test user's (Emily Garcia) properties and confirmed she belonged to #Human_Resources and Domain Users, validating her as a legitimate HR test account.
- I signed into a Windows 11 client as Emily Garcia and opened Settings > Bluetooth & devices > Printers & scanners.
- I clicked "Add a printer or scanner," and Windows automatically discovered "Microsoft MS-XPS Class Driver 2 on HOUTECH" without any manual path entry.
- I clicked Add device and watched the status change to "Connecting."
- Windows confirmed: "You've successfully added Microsoft MS-XPS Class Driver 2 on Houtech.Houtech.local," noting it used the Microsoft enhanced Point and Print driver.
- I did a final check on the printer's settings page and confirmed its status showed Idle, with options to open the print queue, print a test page, and adjust preferences — confirming it was fully ready for day-to-day use.

# Conclusion

- The Print and Document Services role was installed and configured successfully
- A new printer was created, shared, and published to Active Directory
- Access was locked down to the HR department only, removing the default "Everyone" permission
- End-to-end testing from a real user account confirmed the setup worked exactly as intended
