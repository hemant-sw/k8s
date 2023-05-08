What is Linux ?

Linux® is an open source operating system (OS). An operating system is the software that directly manages a 
system's hardware and resources, like CPU, memory, and storage. The OS sits between applications and hardware
and makes the connections between all of your software and the physical resources that do the work.

Linux terminoloogies -

1 - Kernels 
2 - distribution
3 - boot loader
4 - service 
5 - file system
6 - X windows
7- desktop environement
8 - command line

Kernels - It basically acts as an interface between user applications and hardware. The major aim of kernel is to manage communication between software i.e. user-level applications and hardware i.e., CPU and disk memory. kernel is a heart of any operating system which basically manages the 
   - Device management
   - Memory management
   - Process mangagement
   - Handling system calls

   Types of kernels -
     1 - Monolithic kernels
     2 - microlithic kernels
     3 - hybrid kernels

Distribtutions -  It is a version of the Linux operating system that includes a collection of software applications, tools, and utilities that are bundled together into a complete package.

     Example - Debian , UBuntu , mint , centOS ,RHEL etc


Boot Loader - A bootloader is a program that loads and starts the operating system (OS) on a computer or mobile device. It is responsible for initializing hardware components, verifying the integrity of the OS, and loading it into memory

     Example - GRUB , UEFI , Linux loader.


Services - a service is a program or set of programs that runs as a background process , providing specific functions or capabilities to the system or other programs. These services are typically started automatically when the system boots up and continue to run until the system is shut down or the service is manually stopped.

Filesystem - the file system in Linux is a crucial component of the operating system that allows the system to store, organize, and access data on storage devices.

X windows system - graphical subsystem in all linux system.

Desktop environment - Is is the graphical UI on top of the  operating system 
     Example - GNOME ,KDE , XFCE


Command line - tool that is used to type the command on top of the operating system.

SHELL - It provide a powerfull and flexisible way to interact with operating system with CLIs

       Types -
       - Bourne Shell (sh shell)
       - C shell
       - Z shell
       - Bourne Again shell (BASH)

System Startup Process - The system startup process is the sequence of events that occur when a computer or other electronic device is turned on or rebooted. The specific steps involved in the startup process can vary depending on the type of device and the operating system being used, but generally follow a similar pattern. Here is a general overview of the system startup process:

        - Power on self-test (POST): When the device is turned on, the first thing that happens is the power on self-test. This is
          a series of diagnostic checks that the hardware performs to make sure everything is working properly. If any issues are detected during the POST, an error message will be displayed.

        - boot -loader: After the POST is complete, the boot loader program takes over. The boot loader is responsible for loading
          the operating system into memory. Depending on the device and operating system, the boot loader may also perform other tasks such as configuring hardware and loading drivers.

        - Kernel initialization: Once the operating system is loaded into memory, the kernel initializes. The kernel is the core
          of the operating system and is responsible for managing system resources such as memory, CPU, and input/output operations.

        - System services and daemons: After the kernel is initialized, system services and daemons are started. These are
          programs that run in the background and provide various functions and services to the operating system and applications.

        - User login: Once the system services and daemons are running, the user login screen is displayed. The user can then log
          in to the system and start using applications.

        - Startup applications: Finally, any startup applications specified by the user or configured to run automatically by the
          operating system are launched. These may include email clients, web browsers, and other applications that the user wants to have running when they first log in.


Why Linux ?

Most DevOps tools have a requirement for Linux because many new tools of Devops first launched for Linux then after that for other operating system like Windows.
   Example - Docker when first lauched it was lauched for linux in 2013 then after 3 years in 2016 it was lauched for windows.
           - Ansible can not run on windows host natively.it can run on windows under Windows subsystem for linux(WSL).
           - In kubernetes cluster master nodes can only be linux system.




 - To know the shell type use this command 
 <echo $SHELL>

 - Basic Commands
   1 - <echo hi>
       hi <= print message on screen
   2 - <ls>
       List all the directories
   3 - <cd>
       Change directory
   4 - <pwd>
       Print present working directory
   5 - <mkdir>
       create new directory
   6 - To run multiple commands separate each by a semicolon
       <mkdir one ; pwd ; echo hi>    
   7 - To make hierarichal directories 
       <mkdir -p C:\Users\Lenovo\Desktop\dust\dustbin>
   8 - To remove a directory 
       <rm -r C:\Users\Lenovo\Desktop\dust\dustbin>
   9 - To copy a directory 
       <cp -r C:\Users\Lenovo\Desktop\dust\dustbin>
   - Files
   10 - To create a file
       <touch file.txt>
   11 - To create a file with multiline message 
        <cat file.txt>
   12- To view all the files with date and time 
        <ls -ltr>     
   13 - To save password in the terminal
        <export passord='your_password'>
        to access that password use
        <$password>

 Vi text editor => he default editor that comes with the UNIX operating system is called vi (visual editor). 
 Using vi editor, we can edit an existing file or create a new file from scratch. we can also use this editor to just read a text file

=> To start a vi editor use this command
   <vi index.html>
=> To start insert mode type lowercase <i> after that you can easily modify the files content to switch back from the insert mode use
   <escape> button
=> To move around the page use arrow keys or k,h,j,l
=> TO delete a charater use x or to delete an entire line use dd.
=> To copy a line ues yy and to paste a line use p
=> To scroll page up or down use ctrl + u and crtl + d
=> : colol takes you to the propmt where you can type commands
=> To save the command use :w
=> To discard the changes use or quit :q
=> TO save the changes and quit use :wq


Linux command for user accounts

1 => <whoami>  tells user name

2 => <id> tells more details about the user

3 => To switch from  one user to another use <su username>

4 => you can not root user as a root user and root user has no restriction thats why access to the root user is restricted for that use this command 
<sudo ls /root >

Whenever you get permission denied errors it could be because of sudo previleges


Commnad which help to download files =>

1 => To download images , packages etc. you can use 
     <curl url_of_file -o>
     You can also use 
     <wget url -O>

TO check the OS version

1 => use this command to know about OS
     ls /etc/*release*

2 => TO know more detail about OS
     cat /etc/*release*

Package management =>
Ubuntu features a comprehensive package management system for installing, upgrading, configuring, and removing software.


Advanced Packaging Tools (APT)

=> To install a package 
   <sudo apt install nmap>

   You can specify multiple packages to be installed or removed, by separating them with spaces.

=> To Remove a package
   <sudo apt remove nmap>

   Adding the --purge option to apt remove will remove the package configuration files as well. This may or may not be the desired effect, so use with caution

=> Update the package index 
   <sudo apt update>

=> Upgrade packages
   <sudo apt upgrade>











