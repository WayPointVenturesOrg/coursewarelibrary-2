---
lab:
    title: 'Lab: Install and configure Hyper-V'
    module: 'Module 5: Installing and configuring Hyper-V and virtual machines'
---

# Lab: Install and configure Hyper-V

## Scenario

IT management at Contoso Ltd. is concerned about the low utilization of many of the physical servers that are deployed in the London datacenter. Contoso also is exploring options for expanding into multiple branch offices and deploying servers in public and private clouds. For this purpose, the organization is exploring the use of virtual machines.

You will validate the Hyper-V server role, configure virtual machine storage and networking, and deploy the virtual machines. 

## Objectives

- Verify the installation of the Hyper-V server role
- Configure Hyper-V networks
- Create and configure virtual machines
- Enable nested virtualization

## Estimated time: 60 minutes

## Exercise 1: Verify the installation of the Hyper-V server role

### Scenario

The first step in migrating to a virtualized environment is to install the Hyper-V server role on a new server. Because this role is installed already on LON-SVR1, you need to verify the presence of the Hyper-V role.

The main task for this exercise are as follows:

- Verify and configure the Microsoft Hyper-V server role.

### Task 1: Verify and configure the Microsoft Hyper-V server role

1. On **LON-SVR1**, sign in as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select **Start**, and then select **Server Manager**.

3. In Server Manager, select **Tools**, and then select **Hyper-V Manager**.

4. In **Hyper-V Manager**, select **LON-SVR1**, and then select **Hyper-V Settings**.

5. In the **Hyper-V Settings for** **LON-SVR1** window, select each of the available settings and review the description.

6. In the settings list, select **Virtual Hard Disks**.

7. In the **Virtual Hard Disks** page, select **Browse**. 

8. Browse to and select **E:\\VirtualMachines**, and then select the **Select Folder** button.

9. In the settings list, select **Virtual Machines**.

10. In the **Virtual Machines** page, select **Browse**. 

11. Browse to and select **E:\\VirtualMachines**, and then select the **Select Folder** button.

    > You have now specified the default folder for storing Virtual Hard Disks and Virtual Machine files.

12. Select **OK** to close the **Hyper-V Settings for** **LON-SVR1** window.


### Results

After completing this exercise, you should have successfully verified the presence and configuration of the Hyper-V server role on LON-SVR1.

## Exercise 2: Configure Hyper-V networks

### Scenario

After installing the Hyper-V server role on the new server, you must configure the virtual networks. To see the differences between the different network types, you must create an external, internal, and private network.

The main tasks for this exercise are as follows:

1. Create an external network.
2. Create a private network.
3. Create an internal network.

### Task 1: Create an external network

1. In **Hyper-V Manager**, select **LON-SVR1**, and then in the **Actions** pane, select **Virtual Switch Manager**.

2. In the **Virtual Switch Manager for LON-SVR1** window, select **New virtual network switch**.

3. In the **Create virtual switch** pane, select **External**, and then select **Create Virtual Switch**.

4. In the **Virtual switch Properties** pane, in the **Name** text box, enter **Physical Network**.

5. In the **Connection type** area, select **External network**. 
6. In the drop-down menu, select **Microsoft Hyper-V Network Adapter #3**.
7. Ensure that the **Allow management operating system to share this network adapter** check box is selected, and then select **OK**.
8. In the **Apply Networking Changes** dialog box, read the warning that displays, and then select **Yes**.

9. Switch to **Server Manager**, select **Local Server**, and verify that there is a network adapter named **vEthernet** **(Physical Network)**.


### Task 2: Create a private network

1. On **LON-SVR1**, in **Hyper-V Manager**, in the **Actions** pane, select **Virtual Switch Manager**.

2. In the **Virtual Switch Manager for LON-SVR1** window, select **New virtual network switch**.

3. In the **Create virtual switch** pane, select **Private**, and then select **Create Virtual Switch**.

4. In the **Virtual Switch** **Properties** pane, in the **Name** text box, enter **Isolated Network**.

5. In the **Connection type** area, verify that **Private network** is selected, and then select **OK**.

6. In **Server Manager**, verify that no new network adapter has been added. A private network is not connected to any physical network adapter on the host machine.


### Task 3: Create an internal network

1. On **LON-SVR1**, in **Hyper-V Manager**, in the **Actions** pane, select **Virtual Switch Manager**.

2. In the **Virtual Switch Manager for LON-SVR1** window, select **New virtual network switch**.

3. In the **Create virtual switch** pane, select **Internal**, and then select **Create Virtual Switch**.

4. In the **Virtual Switch Properties** pane, in the **Name** text box, enter **Host Internal Network**.

5. In the **Connection type** area, verify that **Internal network** is selected, and then select **OK**.

6. In **Server Manager**, verify that a new network adapter named **vEthernet** **(Host Internal Network)** has been created and is using DHCP to obtain a network address.

   > You may need to refresh **Server Manager** to validate the changes.

### Results

After completing this exercise, you should have successfully configured an external, internal, and private network.

## Exercise 3: Create and configure virtual machines

### Scenario

To view the differences between Generation 1 and Generation 2 virtual machines, you will create two new virtual machines. You will install the Generation 2 virtual machine from Windows Server 2022 installation media. You will create the Generation 1 virtual machine by using a differencing disk from a base image created from an earlier project.

The main tasks for this exercise are as follows:

1. Create a Generation 2 virtual machine.

2. Create a Generation 1 virtual machine.

3. Configure virtual machines.

4. Create checkpoints.

5. Enable host resource protection.

6. Export a virtual machine.

### Task 1: Create a Generation 2 virtual machine

1. On **LON-SVR1**, on the taskbar, select **File Explorer**.

2. In File Explorer, browse to **E:\VirtualMachines**.

3. In File Explorer, select the **Home** tab, and then select the **New Folder** icon twice to create two new folders. 

4. Right-click or access the context menu for each folder, and rename them as follows:

   - **LON-GUEST1**
   - **LON-GUEST2**

5. Close File Explorer.

6. In **Hyper-V Manager**, in the **Actions** pane, select **New**, and then select **Virtual Machine**.

7. In the **New Virtual Machine** **Wizard**, on the **Before You Begin** page, select **Next**.

8. On the **Specify Name and Location** page, select **Store** **the virtual machine in a different location**, enter the following values, and then select **Next**:

   - Name: **LON-GUEST2**

   - Location: **E:\\VirtualMachines\\LON-GUEST2\\**

9. On the **Specify Generation** page, select **Generation 2**, and then select **Next**.

10. On the **Assign Memory** page, in the **Startup memory** box, enter a value of **1024 MB**, and then select **Next**.

11. On the **Configure Networking** page, select **Isolated Network**, and then select **Next**.

12. On the **Connect Virtual Hard Disk** page, select **Create a virtual hard disk**.

13. In the **Name** text box, enter **LON-GUEST2.vhdx**.

14. In the **Location text** box, enter **E:\\VirtualMachines\\LON-GUEST2**.

15. In the **Size** text box, enter **127**, and then select **Finish**.

16. Right-click or access the context menu for **LON-GUEST2**, and then select **Settings**.

17. In the **Settings for LON-GUEST2 on LON-SVR1** window, in the **Hardware** area, select **SCSI Controller**.

18. In the **SCSI Controller** pane, select **DVD Drive**, and then select **Add**.

19. In the **DVD Drive** area, select **Image** **file**.

20. In the **Image file** text box, enter **E:\\ISOs\\Win2022_Eval.iso**, and then select **Apply**.

21. In the **Hardware** area, select **Firmware**.

22. In the **Boot order** area, select **Network Adapter**, select **Move Down** twice, and then select **OK**.

23. In the **Boot order** area, select **DVD Drive**, select **Move Up** to move it to the top of the list, and then select **OK**.

24. Right-click or access the context menu for **LON-GUEST2**, and then select **Connect**.

25. In the **LON-GUEST2 on LON-SVR1 – Virtual Machine Connection** window, select **Start**.

26. When prompted, press any key to boot from DVD.

    > If you miss the prompt, you may need to reset the VM and try a second time to press any key to boot from DVD.

27. In the **Microsoft Server Operating System Setup** window, select **Next**, and then select **Install now**.

28. On the **Select the operating system you want to install** page, select **Windows Server 2022 Datacenter Evaluation**, and then select **Next**.

    > The Windows Server 2022 Datacenter Evaluation option installs the core version of Windows Server. The core version does not contain any GUI interface.

29. On the **Applicable notices and license terms** page, select the **I accept the license terms** check box, and then select **Next**.

30. On the **Which type of installation do you want** page, select **Custom: Install Windows only (advanced)**.

31. On the **Where do you want to install Windows** page, select **Drive 0 Unallocated Space**, and then select **Next**.

    > **Note:** The operating system begins to install. Installation will take a few minutes and the virtual machine restarts as needed.

32. After installation completes, read the message about changing the Administrator password, select **OK** and press Enter.

    > **Note:** You may need to enter Ctrl-Alt-Del first to unlock the screen.

33. In the **`New password`** and **`Confirm password`** fields, enter **`Pa55w.rd`**, and then press Enter twice to acknowledge the password has been changed.

    > After a few moments the Server Configuration tool (**sconfig**) starts automatically and presents the server management screen.

34. After the installation is complete, in the **LON-GUEST2 on LON-SVR1 – Virtual Machine Connection** window, select **Shut Down**, and then select **Shut Down** again to confirm. 

35. Close the **LON-GUEST2 on LON-SVR1 – Virtual Machine Connection** window.

### Task 2: Create a Generation 1 virtual machine

1. In **Hyper-V Manager**, in the **Actions** pane, select **New**, and then select **Hard Disk**.

2. In the **New Virtual Hard Disk** **Wizard**, on the **Before You Begin** page, select **Next**.

3. On the **Choose Disk Format** page, select **VHD**, and then select **Next**.

4. On the **Choose Disk Type** page, select **Differencing**, and then select **Next**.

5. On the **Specify Name and Location** page, specify the following details, and then select **Next**:

   - Name: **LON-GUEST1.vhd**

   - Location: **E:\\VirtualMachines\\LON-GUEST1\\**

6. On the **Configure Disk** page, enter **E:\\VirtualMachines\\ServerCoreBase.vhd** as the location, and then select **Finish**.

7. Select **Start**, and then select the **Windows PowerShell ISE** icon.

8. At the **Windows PowerShell** command prompt, enter the following command to create a new virtual machine named **LON-GUEST1**, and then press Enter:

   ```
   New-VM –Name LON-GUEST1 –MemoryStartupBytes 1024MB –VHDPath “E:\VirtualMachines\LON-GUEST1\LON-GUEST1.vhd” –SwitchName "Isolated Network"
   ```

9. Close the **Windows PowerShell ISE** window.


### Task 3: Configure virtual machines

1. On **LON-SVR1**, in **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST1**, and then select **Settings**.

2. In the **Settings for LON-GUEST1 on LON-SVR1** window, note the list of hardware for **LON-GUEST1**.

3. In the **Hardware** area, select **Memory**.

4. Select the **Enable Dynamic Memory** check box.

5. In the **Maximum RAM** box, enter **4096**.

6. In the **Hardware** area, select **Network Adapter**.

7. In the **Bandwidth Management** area, select the **Enable bandwidth management** check box.

8. In the **Minimum bandwidth** text box, enter **10**.

9. In the **Maximum bandwidth** text box, enter **100**.

10. In the **Management** area, select **Integration Services**.

11. Select the **Guest services** check box, and then select **OK**.

    > **Note:** You must have completed the previous tasks in this exercise before you can continue. This includes shutting down **LON-GUEST2**.

12. In **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST2**, and then select **Settings**.

13. In the **Settings for LON-GUEST2 on LON-SVR1** window, note the list of hardware for **LON-GUEST2**. Note the differences from **LON-GUEST1**.

14. In the **Hardware** area, select **Security**, and then take note of the settings that are available.

15. In the **Hardware** area, select **Memory**.

16. Verify that the **Enable Dynamic Memory** check box is not selected.

17. In the **Hardware** area, expand **Hard Drive**, and then select **Quality of Service**.

18. Select the **Enable Quality of Service management** check box.

19. In the **Minimum** text box, enter **10**.

20. In the **Management** area, select **Integration Services**.

21. Select the **Guest services** check box, and then select **OK**.


### Task 4: Create checkpoints

1. On **LON-SVR1**, in **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST2**, and then select **Checkpoint**.

   > Notice that a checkpoint is created and displayed in the **Checkpoints** pane.

2. Right-click or access the context menu for **LON-GUEST2**, and then select **Start**.

3. Right-click or access the context menu for **LON-GUEST2**, and then select **Connect**.

4. On **LON-GUEST2**, sign in as **Administrator** using **Pa55w.rd** as the password.

5. Switch to **LON-SVR1**.

6. On **LON-SVR1**, in **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST2**, and then select **Settings**.

7. In the **Settings for LON-GUEST2 on LON-SVR1** window, in the **Hardware** area, select **Add Hardware**.

8. In the **Add Hardware** area, select **Network Adapter**, and then select **Add**.

9. In the **Network adapter** area, in the **Virtual switch** box, select **Host Internal Network**, and then select **OK**.

10. On **LON-SVR1**, in **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST2**, and then select **Checkpoint**.

11. Read the information in the **Virtual Machine Checkpoint** window, and then select **OK**.

12. Right-click or access the context menu for the most recent checkpoint, and then select **Apply**.

13. In the **Apply Checkpoint** dialog box, select **Apply**.

14. Verify that the **Status for LON-GUEST2** is **Off** because it was a production checkpoint.


### Task 5: Enable host resource protection

1. On **LON-SVR1**, select the **Start** button, and then select **Windows PowerShell ISE**.

2. In **Windows PowerShell**, at the command prompt, enter the following command, and then press Enter:

   ```
   Set-VMProcessor LON-GUEST2 -EnableHostResourceProtection $true
   ```

3. Close the **Windows PowerShell ISE** window.


### Task 6: Export a virtual machine

1. On **LON-SVR1**, in **Hyper-V Manager**, right-click or access the context menu for **LON-GUEST2**, and then select **Export**.

2. In the **Export Virtual Machine** dialog box, in the **Location** text box, enter **E:\VirtualMachines\Guest2-Bak**, and then select **Export**.


### Results

After completing this exercise, you should have successfully created and configured both a Generation 1 virtual machine and a Generation 2 virtual machine.

## Exercise 4: Enable nested virtualization

### Scenario

You are considering the use of nested virtualization for your development environment. You decide to enable nested virtualization for the LON-GUEST1 virtual machine. 

The main tasks for this exercise are as follows:

1. Enable nested virtualization.

2. Enable Hyper-V on LON-GUEST1.

### Task 1: Enable nested virtualization

1. On **LON-SVR1**, select **Start** and then select **Windows PowerShell ISE**.

2. On LON-SVR1, at the **Windows PowerShell** prompt, enter the following command, and then press Enter:

   ```
   Set-VMProcessor -VMName LON-GUEST1 -ExposeVirtualizationExtensions $true
   ```

3. Enter the following command, and then press Enter:

   ```
   Get-VMNetworkAdapter -VMName LON-GUEST1 | Set-VMNetworkAdapter -MacAddressSpoofing On
   ```

4. Enter the following command, and then press Enter:

   ```
   Set-VM -VMName LON-GUEST1 -MemoryStartupBytes 4GB
   ```

### Task 2: Enable Hyper-V on LON-GUEST1

1. On **LON-SVR1**, at the **Windows PowerShell ISE** prompt, enter the following command, and then press Enter:

   ```
   Start-VM LON-GUEST1
   ```

2. Wait until **LON-GUEST1** has started, enter the following at the Windows PowerShell prompt, and then press Enter.

   ```
   Enter-PSSession -VMName LON-GUEST1
   ```

3. When you receive a prompt, sign in as **Contoso\\Administrator** by using **Pa55w.rd** as the password.

4. Enter the following command, and then press Enter:

   ```
   Install-WindowsFeature -Name Hyper-V -IncludeAllSubFeature -IncludeManagementTools -Restart
   ```

5. Wait for **LON-GUEST1** to restart. The virtual machine might restart several times.

6. Connect to **LON-GUEST1** and sign in as **Administrator** by using **Pa55w.rd** as the password. 

   > The Server Configuration tool (SConfig) starts automatically.

7. At the menu screen enter `15` and then press Enter to exit to the PowerShell command line.

8. At the command line enter `Get-WindowsFeature Hyper*` and then press Enter.

   > Notice that the Hyper-V feature is installed as indicated by the `X` selection.
   >

9. In the **LON-GUEST1 on LON-SVR1 – Virtual Machine Connection** window, select **Shut Down**, and then select **Shut Down** again to confirm. 

10. Close the **LON-GUEST1 on LON-SVR1 – Virtual Machine Connection** window.

### Results

After completing this exercise, you should have successfully configured a virtual machine for nested virtualization.
