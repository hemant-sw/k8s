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

   So whenever you are running a container always run as non-root because if anyone breaks this he still in this specific namespace he won't be as root 
 

 


      



