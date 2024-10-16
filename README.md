# Active Directory File Share Permissions and Security Group Management

## Lab Overview
This Lab involved setting up and testing file share permissions on a Domain Controller (DC-1) and verifying access rights for different user groups. The goal was to ensure that security groups and folder permissions were properly configured and tested, including the creation of a security group for accounting and testing its access rights.

## Steps Performed

### 1. Turning on DC-1 and Client-1 Virtual Machines (VMs)

1. **Turn on VMs**  
   Logged into the **Azure Portal** and started the **DC-1** and **Client-1** virtual machines to begin the project.

  
### 2. Creating File Shares and Setting Permissions

1. **Create Sample Folders on DC-1**  
   Logged into **DC-1** as the domain admin account `mydomain.com\jane_admin`.  
   Created the following folders on the `C:\` drive of DC-1:
   - `read-access`
   - `write-access`
   - `no-access`
   - `accounting`
   
  <img width="566" alt="Screenshot 2024-10-16 142622" src="https://github.com/user-attachments/assets/611873ba-6f53-4b2d-b147-0257afe59c4b">


2. **Set Folder Permissions**  
   Set the following permissions for the created folders:
   - **read-access:** Granted **"Domain Users"** group **Read** permissions.
   - **write-access:** Granted **"Domain Users"** group **Read/Write** permissions.
   - **no-access:** Granted **"Domain Admins"** group **Read/Write** permissions.
   - **accounting:** Permissions not set yet.
   - 
<img width="611" alt="Screenshot 2024-10-16 142259" src="https://github.com/user-attachments/assets/66f95d58-9aa5-4365-9de4-53e89d174fbf">




### 3. Testing File Share Access as a Normal User
1.  **Share the Folders**  
      Shared the folders on the network so they could be accessed from **Client-1**.


2. **Log into Client-1 as a Normal User**  
   Logged into **Client-1** using a normal user account (e.g., `mydomain\someuser`).

3. **Access the Shared Folders**  
   From **Client-1**, used **Run (Windows + R)** and typed `\\dc-1` to access the shared folders.  
   Attempted to access each of the folders:
   - **read-access:** Successfully accessed and viewed the contents but could not write to it.
   - **write-access:** Successfully accessed and was able to create new files/folders.
   - **no-access:** Access was denied.
   
   The folder permissions worked as expected based on the configurations.

   
  <img width="575" alt="Screenshot 2024-10-16 120457" src="https://github.com/user-attachments/assets/ea23f02f-b010-4139-afe7-1c677226f6be">

### 4. Creating and Testing the ACCOUNTANTS Security Group

1. **Create ACCOUNTANTS Security Group**  
   Logged back into **DC-1** as `mydomain.com\jane_admin`.  
   Created a new security group in **Active Directory** called **"ACCOUNTANTS"**.
   
<img width="578" alt="Screenshot 2024-10-16 142928" src="https://github.com/user-attachments/assets/c011d779-9133-4ef3-b8a2-d2fe8004d683">


3. **Set Permissions for the ACCOUNTING Folder**  
   Set the following permissions for the **accounting** folder:
   - Group: **ACCOUNTANTS**
   - Permissions: **Read/Write**
   - 
<img width="590" alt="Screenshot 2024-10-16 143717" src="https://github.com/user-attachments/assets/bef0f43b-d9d7-4547-ac0d-67c5265d4d43">


4. **Testing Access to the ACCOUNTING Folder as a Normal User**  
   Logged back into **Client-1** as `mydomain\someuser`.  
   Attempted to access the **accounting** folder from `\\dc-1`. Access was denied as expected because `someuser` was not a member of the **ACCOUNTANTS** group.

   

5. **Add someuser to the ACCOUNTANTS Group**  
   Logged back into **DC-1** and added `someuser` to the **ACCOUNTANTS** security group in Active Directory.


<img width="570" alt="Screenshot 2024-10-16 143404" src="https://github.com/user-attachments/assets/a3e64728-436c-49b3-884e-29dd85112247">


6. **Re-test Access to the ACCOUNTING Folder**  
   Signed back into **Client-1** as `someuser` and tried accessing the **accounting** folder again. This time, access was successful, and I was able to read and write to the folder as per the permissions.



## Conclusion
This lab demonstrated how to configure file share permissions in Active Directory and use security groups to control access. The successful creation of a security group, application of permissions, and testing of access rights provided a solid foundation for managing file security within a domain environment.
