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
      



