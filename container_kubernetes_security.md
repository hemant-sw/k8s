container-
            Isolation in the same system with unique namespaces.

            PID - Isolation of process ids
            User - Isolation of users & UIDs
            Mount - Isolation of mount points
            Net - Isolation of networking interfaces & environment
            UTS - Isolation of hostname
            IPC - Isolation of IPC traffic
            Cgroup - Isolation of cgroups (memory & cpu)



Container security - whatever things you run inside  the container they are available in
                     host machine and also executable directly from there.

                   - Container are just isolated environment and they are not secure 
                     it is not like something happens in container it is only going to affect container.

                   - If container executed in  the wrong way it will also affect host 
                     machine as well . 



Example - 

1- Create a docker conatiner with namespace -
   <docker run --name debugcontainer --rm -it ubuntu bash>

2- Inside that caontainer create a file -
   <echo "inside container" > file.txt>

3- To view content inside the file -
   <cat file.txt>
   you can see the message "inside container"

You can access same file from host machine by this following this steps

1- Run this command 
   <docker inspect debugcontainer | grep dir -i>
   you can see there are multiple directories running 
   From this we will choose "upperDir" and copy the path

2 - Change directory to that path
    <cd pathName>
    when you ls you can see file.txt from there also

3- Cat to that file and you can see the same message "inside container" from host machine also.



What does it mean to Root inside the container -

=> Run this commands -

=> TO Root on host machine & root inside the container by using this commands-

   1 - run this docker command-
       <docker run --rm -it nginx bash>

   2 - In bash sleep it for 1 day
       <sleep 1d>

   3 - after that when you go to the main tab run this command -
       <ps -ef | grep sleep>
       you can see that above one is exectted as a root user.

=>  To non-Root on host machine & root inside the container by using this commands-
   
   1 - <adduser ubuntu>
   2 - <sudo chown ubuntu:ubuntu /var/run/docker.sock>
   3 - <su - ubuntu>
   4 - <docker run --rm -it nginx bash>
   5 - <sleep 2d>

   When you again run sleep command -

      <ps -ef | grep sleep>
      then you can see both (sleep 1d and sleep 2d) both executed as a root user despite running as ubuntu this is because in 
      background docker deamon running as root user so it does not matter you running from ubuntu user or any other user all proceess are executed as a root.
      Since docker daemon runs as root, eventually all the processes triggered by it run as root.

=> Root on host machine & non-root inside container.

   <docker run --rm --user 1000:1000 -it nginx bash>
   <sleep 3d>

   after that when you again running  sleep command -
   <ps -ef | grep sleep>
   Now you can see that sleep 3d running as a non-root user

   So whenever you are running a container always run as non-root because if anyone breaks this he still in this specific namespace so  he won't be as root.


Privileged container - Running a privileged container has more access to the host then the normal container.



=> By default container runtimes go to great lengths to shield a container from the host system. Running in --privileged mode disables/bypasses most of these checks. This basically means that if you are root in a container you have the privileges of root on the host system. Is is only meant for special cases such as running Docker in Docker and should be avoided.


=> running containers in privileged mode is really a bad idea because  privileged container system with root access gives you access to the host filesystem, kernel settings and processes.

=> Kernel files are very importent file on host machine we are going to see how we can mess with it.

Swappiness - This control is used to define how aggressive the kernel will swap
memory pages.  Higher values will increase aggressiveness, lower values
decrease the amount of swap.  A value of 0 instructs the kernel not to
initiate swap until the amount of free and file-backed pages is less
than the high water mark in a zone.

=> By default swappiness value of host machine is 60.

=> To know the swappiness value of your host machine use this command-

   <cat /proc/sys/vm/swappiness>

   You can change the swapiness value of the container by running container in a priviledge container , to do that you can follow this step.

   1 - <docker run --rm --privileged -it ubuntu bash>

       you are now running a contaienr in privilige mode.
       
   2 - Now lets try to edit the swappiness value.
       
       <cat /proc/sys/vm/swappiness> 
       
       at present the swappiness value is 60 or in killerkoda it will be 0.

   3 - { echo 10 > /proc/sys/vm/swappiness }

       after changing this the swapiness value will be zero.

       => These kind of changes to the kernel files can create DoS attacks!

   4 - How to know we are running a normal container or a priviledge contaienr run two containers, one normal & one privileged

      <docker run --rm -it ubuntu bash>
      <docker run --rm --privileged -it ubuntu bash>
         1- By Checking for mount permissions & masking.
           <mount | grep 'ro,'>
           <mount | grep /proc.*tmpfs>

       when you check the mount point in normal container all the information is in read only format but in previleged container
       it will not in read only you can edit those.
         2 - Linux capabilities - we will see more about it in the next section!
             <capsh --print>

             In normal container you have more number of capailities but in preveledged container you have lesser nomber of capabilities means you can do various other
             things in preveleged container.



capabilities - The purpose of performing permission checks, traditional UNIX implementations distinguish two categories of processes:
       privileged processes (referred to as superuser or root ,whose effective UID is zero), and unprivileged processes (whose
       effective UID is nonzero).  Privileged processes bypass all kernel permission checks, while unprivileged processes are
       subject to full permission checking .

       => There are various types of capalities some of them are -

          CAP_AUDIT_CONTROL
          CAP_AUDIT_READCAP_AUDIT_READ
          CAP_AUDIT_WRITE

      =>  The goal of capabilities is divide the power of superuser into
          pieces, such that if a program that has one or more
          capabilities is compromised, its power to do damage to the
          system would be less than the same program running with root
          privilege.

      =>  To print all the capabilities use this command -
          <capsh --print>









 

 


      



