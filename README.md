[TryHackMe | File Inclusion](https://tryhackme.com/room/fileinc)

# TryHackMe-File-Inclusion
'**File Inclusion:**  This room introduces file inclusion vulnerabilities, including Local File Inclusion (LFI), Remote File Inclusion (RFI), and directory traversal.`

## Task 1 Introduction
![image](https://user-images.githubusercontent.com/58542375/173562517-0fd0332f-1dcf-4eb6-930b-ea733680e0e7.png)

## Task 2 Deploy the VM

## Task 3 Path Traversal
[PHP: file_get_contents - Manual](https://www.php.net/manual/en/function.file-get-contents.php)

![image](https://user-images.githubusercontent.com/58542375/173564652-1c6871a3-35a5-418b-abe1-72241193152e.png)

![image](https://user-images.githubusercontent.com/58542375/173564886-67831530-4ba2-4445-ab51-e538e0af6a93.png)

![image](https://user-images.githubusercontent.com/58542375/173565211-10cb2f8f-3fb7-47a1-ae36-4de62e541d07.png)

*dot-dot-slash attack*

`http://webapp.thm/get.php?file=../../../../etc/passwd`

`http://webapp.thm/get.php?file=../../../../boot.ini`

`http://webapp.thm/get.php?file=../../../../windows/win.ini`

```
C:\Windows>cd ..

C:\>dir *.ini
 Volume in drive C is Windows
 Volume Serial Number is BADE-41F7

 Directory of C:\

File Not Found
```

```
C:\Windows>dir *.ini
 Volume in drive C is Windows
 Volume Serial Number is BADE-41F7

 Directory of C:\Windows

07-Jun-20  03:31 PM            37,625 cfgall.ini
06-Jun-18  02:44 AM               219 system.ini
06-Jun-18  02:44 AM                92 win.ini
               3 File(s)         37,936 bytes
               0 Dir(s)  45,286,510,592 bytes free

C:\Windows>type win.ini
; for 16-bit app support
[fonts]
[extensions]
[mci extensions]
[files]
[Mail]
MAPI=1
```

|Location|Description|
|----------|------------|
|/etc/issue| contains a message or system identification to be printed before the login prompt.|
|/etc/profile|controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived|
|/proc/version|specifies the version of the Linux kernel|
|/etc/passwd|has all registered user that has access to a system|
|/etc/shadow|contains information about the system's users' passwords|
|/root/.bash_history|contains the history commands for root user|
|/var/log/dmessage|contains global system messages, including the messages that are logged during system startup|
|/var/mail/root|all emails for root user|
|/root/.ssh/id_rsa|Private SSH keys for a root or any known valid user on the server|
|/var/log/apache2/access.log|the accessed requests for Apache  webserver|
|C:\boot.ini|contains the boot options for computers with BIOS firmware|

## Task 4 Local File Inclusion - LFI
![image](https://user-images.githubusercontent.com/58542375/173569223-618fb0a2-c5c9-4e79-9465-9622322ab422.png)

![image](https://user-images.githubusercontent.com/58542375/173571368-0162dbef-2b3f-41af-918d-c39c119c0773.png)

## Task 5 Local File Inclusion - LFI #2
*NullByte* `%00`

![image](https://user-images.githubusercontent.com/58542375/174087161-2dee0f9f-8598-41fd-a854-6ed4d85f0756.png)

![image](https://user-images.githubusercontent.com/58542375/174087424-cea7c291-3b65-42d1-b17c-289866414575.png)

`include("languages/../../../../../etc/passwd%00").".php");`

![image](https://user-images.githubusercontent.com/58542375/174106633-be705e4f-8bcd-422c-b4c9-973577bce1d9.png)

![image](https://user-images.githubusercontent.com/58542375/174107025-413f758e-caa8-4734-afb7-e5255d881fa5.png)

![image](https://user-images.githubusercontent.com/58542375/174107409-e3e199de-be90-45ed-8247-49329ab31746.png)

![image](https://user-images.githubusercontent.com/58542375/174108235-f3dd51f4-39c1-42f3-95ee-02d8c618389e.png)

## Task 6 Remote File Inclusion - RFI
*include* function

*allow_url_fopen* **ON**

![image](https://user-images.githubusercontent.com/58542375/174110626-b5e9ddf9-5feb-4c83-8c20-5353495f4ade.png)

`http://10.10.90.61/playground.php`

![image](https://user-images.githubusercontent.com/58542375/174111739-a9821e44-05ee-4d1d-aad0-5c07d2d04523.png)

## Task 7 Remediation
1. Keep system and services, including web application frameworks, updated with the latest version.
2. Turn off PHP errors to avoid leaking the path of the application and other potentially revealing information.
3. A Web Application Firewall (WAF) is a good option to help mitigate web application attacks.
4. Disable some PHP features that cause file inclusion vulnerabilities if your web app doesn't need them, such as allow_url_fopen on and allow_url_include.
5. Carefully analyze the web application and allow only protocols and PHP wrappers that are in need.
6. Never trust user input, and make sure to implement proper input validation against file inclusion.
7. Implement whitelisting for file names and locations as well as blacklisting.

## Task 8 Challenge
### Steps for testing for LFI
1. Find an entry point that could be via GET, POST, COOKIE, or HTTP header values!
2. Enter a valid input to see how the web server behaves.
3. Enter invalid inputs, including special characters and common file names.
4. Don't always trust what you supply in input forms is what you intended! Use either a browser address bar or a tool such as Burpsuite.
5. Look for errors while entering invalid input to disclose the current path of the web application; if there are no errors, then trial and error might be your best option.
6. Understand the input validation and if there are any filters!
7. Try the inject a valid entry to read sensitive files

![image](https://user-images.githubusercontent.com/58542375/174117112-edfab529-9011-4b89-afb5-e505647eba6e.png)

![image](https://user-images.githubusercontent.com/58542375/174117316-381088f6-5959-4828-adfc-eaeea70ff437.png)

![image](https://user-images.githubusercontent.com/58542375/174117671-f23dd830-330f-44ee-acdc-d1433b9acbc5.png)

![image](https://user-images.githubusercontent.com/58542375/174117968-e42c81f6-48ed-4c1f-a855-3ec8a3b8f1c1.png)
