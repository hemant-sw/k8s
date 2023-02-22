What is Linux ?

Linux® is an open source operating system (OS). An operating system is the software that directly manages a 
system's hardware and resources, like CPU, memory, and storage. The OS sits between applications and hardware
and makes the connections between all of your software and the physical resources that do the work.\

Why Linux ?

Most DevOps tools have a requirement for Linux because many new tools of Devops first launched for Linux then after that for other operating system like Windows.
   Example - Docker when first lauched it was lauched for linux in 2013 then after 3 years in 2016 it was lauched for windows.
           - Ansible can not run on windows host natively.it can run on windows under Windows subsystem for linux(WSL).
           - In kubernetes cluster master nodes can only be linux system.


SHELL Types -
 - Bourne Shell (sh shell)
 - C shell
 - Z shell
 - Bourne Again shell (BASH)

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
        <cat > file.txt>
