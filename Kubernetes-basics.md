 
 <h1>1 - Container management</h1> 
    There are mainy two types of Container management services
    
    1- Monolithic Containers - In this type of container all the  all the services are bundle of in one container
       for example suppose you have application and in that application we have -
        - Frontend 
        - Backend
        - Database
        - Chat
        - networks
       So we have to deploy entire application again if we want to make any modifcation in any specific service of the application 
       which is not a good pratice, Now we dont use this approch.

    2- Micro Services - In Micro services we deploy each services individually like Frontend, Backend, Database.
       So in this approch we dont need to deploy entire application we just deploy a specific service and every container running
       Isolated with their own dependecy and configuration and they are not dependend on other container.

So they are running isolated now we have to do something so they can communicate with each other.

Orchestrator - Orchestrator helps us in deploying and managing container dynamically like - 
                - Deploy
                - Zero-update downtime
                - Scale
                - Self-Healing containers
                    This above are the features of cloud native application

Kubernetes - 
It is the most popular container orchestration tool infact it has more features than orchestation. it allows you to deploy and manage multi-container applications at scale.

Why kubernetes -
    - To monitor them.
    - runing pods on multiple nodes
    - Flexibility
    - Auto scaling 
    - Sheduling
    - Self healing capablities

    ------------------------------------------------------------------------------------------------------------------------------------------------


                    Kubernetes Architeture

Kubernetes clusters -
 Kubernetes cluster is a set of node machines and contrtol plane for running containerized applications. If you're running Kubernetes, you're running a cluster.

 Kubectl -
 Kubectl is a kubeernetes CLI which helps us to communicate with control plane or cluster.

 Control plane - 
 It helps to manage worker nodes control.It helps in controlling entire cluster.It has following things
            1 - API server -
                            The API (application programming interface) server determines if a request is valid and then processes it. 
                            The API is the interface used to manage, create, and configure Kubernetes clusters.
            2 - Scheduler - scheduling refers to making sure that Pods are matched to Nodes so that the kubelet can run them. Preemption is the process 
                            of terminating Pods with lower Priority so that Pods with higher Priority can schedule on Nodes.
            3 - controller managers

            4 - ETCD -
                            Consistent and highly-available key value store used as Kubernetes backing store for all cluster data.

Worker node -

A worker node is a node that runs the application in a cluster and reports to a control plane. The main responsibilities of a worker node is to process data stored in the cluster and handle networking to ensure traffic between the application across the cluster and outside of the cluster are properly facilitated.
it has following components -
            1 - kubelet -
                            An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. 
            2 - kube-proxy - 
                            It maintain network rules on nodes. these networl rules allow you to communicate to pods from network
            3 - Containerd -
                            The Container Runtime Interface (CRI) is the main protocol for the communication between the kubelet and Container Runtime. 
            4 - pods -
                      A pod is the smallest and simplest Kubernetes object.

--------------------------------------------------------------------------------------------------------------------------------------------------------

YAML - 
        - It is most widely used in cloud-native space.
        - Human readable data-serialization language.
        - It is not a markup language.
        - Indentaion matter a lot.


To create a nginx pod
  <kubectl <pod-name> --image=nginx>



Namespaces -
        - namespaces provides a mechanism for isolating groups of resources within a single cluster (cluster in sub-cluster).
        - It will provide isolated environment to the teams. If their are two teams like development team and testing team then 
          they should have different namesapces to work
        - namespaces required to grouping resources separately like monitoring ,database etc.

        - To create a name space use this commmand -
        < kubectl create ns {namespace-name} >

        - Like for example we have created a two namespace of name dev and  
          testing by entering this commands
             - kubectl create ns dev
             - kubectl create ns testing
        
        - we can create pod with same name in two different namspace like below we did in dev and testing namepaces 
             - kubectl create deploy saiyam --image=nginx -n testing
             - kubectl create deploy saiyam --image=nginx -n dev


        - To view all namespaces use this command
             - kubectl get ns

        - To view details of namespace use this command
             - kubectl describe ns {namespace-name}

        - To see declerative of creating a namespace use this command-
             - kubectl create ns demo --dry-run=client -oyaml

        - To delete namespace use this command -
             - kubectl delete namespace {namespace-name}

        - To switch to different namespace use this command
             - kubectl config set-context --current --namespace=dev

Labels and Selectors
        - Kubernetes labels are key-value pairs that can connect identifying metadata with Kubernetes objects. 
          it makes object meaningfull and easy to identify.

        - To Show the label - (for example to check the labels of nginx)
          - kubectl get pods --show-labels

        - To create label use this command 
          - kubectl get pod nginx live=demo

        - In above live is the key and demo is the value.

        - Lables are defined in the metadata section.  


Pods -
       Pods is the smallest unit in entire architecture of kuberneters cluster.
       Container run inside the pod.
       Each pod as assignes a pod IP.
       A single pod can run multiple containers
     
     - To create a pod use this command -
        kubectl run pod-name --image=nginx

     - To see all details of pods like when it is created and when image was pulled & we use this when our pod is not starting .
       kubectl describe pod hemant

     - To go inside the pod to see what inside the pod use this command
       kubectl exec -it pod-name -- sh

       By going inside the pod you can see all things by typing ls and also you can go to differnt directory, to exit from interative terminal just type exit.
       
     - To see more pods information use this command -
       kubectl get pods -owide
     - To delete a pod use this command
       kubectl delete pod pod-name --force

Pod Lifecycle -
     - Pending - 
                finding the node waiting for PV to be ready and PVC to bound to it.

     - ContainerCreating - 
                Pulling images started it attaching network.

     - Running - 
                Pod is running.
     - Error - 

     - Crashloopbackoff - 
                 process dying too many times.
     - Succeeded -
                 when work is completed - jobs etc 


Init containers - 
                 Init containers are the special type of container which run before the main containers they have similar use as regulat containers.

                 To run init container first hit this command
                 vi init 

                 To insert file hit I button and paste this file-


                 after entering this hit escsape button and type colon wq 

                 To apply this file enter this command -
                 kubectl apply -f init

                 By entering this command inside pod init container will be created


Multi-init contaienr - 
                 It helps to run multi init containers.

                 To insesrt yaml file use
                 vi multi
                 kubectl apply -f multi

Multi-Container - 
                 It helps us to create multiple container

                 To insert yaml file use this -
                 vi mc.yaml
                 kubectl apply -f mc.yaml

                 Pod with multi-container created

                 To check all info
                 kubectl describe pod multi-container

                 To view logs of multi-conainer
                 kubectl logs -f multi-container -c nginx-container

                 To know what inside html file
                 kubectl logs -f multi-container -c nginx-container -- curl localhost

Probes - 
        When via service kubernetes sending a traffic to a pod continously. suppose due to any reason (deadlock  or any error) the pod is not ready to handle that much of traffic but here kubernetes doesnot know that the pod is not ready and it keep sending the traffic to the pod this will 
        lead to data inconsistency and not gives proper output to the application so to overcome that situation probes comes into the picture.

        There are 3 types of Probes.
        1 - Readiness probes
        2 - Startup probes
        3 - Liveness probes

        1- Readineses Probes - It will check the pod is ready or not accept  that much of traffic.
                             - It will Check dependecy for the pod in terms of availability of service and latency issue check

        2 - Startup  - first this will execute until it success other probes are not executed

        3 - Liveness probes - http get - if response ok or not 200 -399
                            - tcpsocket - portcheck
                            - exec custom command (like file check ) to check if the pod is ready or not 
                            - kubelet restarts container when liveness fails.

Limits - 
        Limits as the maximum amount of a resource to be used by a container. This means that the container can never consume more than the memory amount or CPU amount indicated.


Request -
        Requests are the minimum guaranteed amount of a resource that is reserved for a container.


        If we ask for more cpu and that much cpu is not present in our system like if we total 2 cpu and we are reauesting for 3 then pod will not run it will be in pending state and scheduler will not start



Deployment - A Kubernetes Deployment is used to tell Kubernetes how to create 
             or modify instances of the pods that hold a containerized application.Deployments can scale the number of replica pods, enable rollout of updated code in a controlled manner, or roll back to an earlier deployment version if necessary.

             Example - It will tell what to do to pods in order that application never goes down

          

ReplicaSet - A ReplicaSet is a process that runs multiple instances of a Pod and keeps the specified number of Pods constant. 
             Its purpose is to maintain the   specified number of Pod instances running in a cluster at any given time to prevent users 
             from losing access to their application when a Pod fails or is inaccessible. 

             ReplicaSet helps bring up a new instance of a Pod when the existing one fails, scale it up when the running instances are not up to the specified number, and scale down or delete Pods if another instance with the same label is created. A ReplicaSet ensures that a specified number of Pod replicas are running continuously and helps with load-balancing in case of an increase in resource usage.

             Example - suppose we have define 2 instances of  pod in repica set if anyone pod goes down then it automatically create new pod. this will ensure that our application never goes down 

           - When we update the deploy image 
             New pod gets created old pod server traffic until it finishes its termination-grace-period (30 by default)     


             How to create a deployment -

             - To create a deployment use this command
               kubectl deploy nginx --image=nginx

               Above command will create a deployment of nginx deployment

             - To get it use this command - 
               kubectl get deploy

               Deployment will internally create a replicaset to check that use this command 
               kubectl get rs

               It also interally create pod to check -
               kubectl get pods 

             - To scale replica use this command
               kubeclt scale deploy nginx --replicas 5 

               Above command will create a 5 pods

             - To update a replica set use this command -
               kubectl edit deploy nginx

               After entering this command you can see yaml file from there you can easliy update it by editing replicas: 3  

               After entering this 2 pods will be terminated

             - To update the image and change to any specific version use this command -
               kubectl set image deployment/nginx nginx=nginx:1.15.2 --record

             - To describe pods what happening inside -
               kubectl describe deploy nginx

             - If you change image to any wrong version then when you check pods you will see message like ErrImagePull means it unable to pull the image for example -

               kubectl set image deployment/nginx nginx=nginx:Hemant --record

               After that when you check pods you will see error image pull message

             - To see roll out status that how many replicas are update use this command -
               kubectl rollout status deploy nginx

             - To see Roll out history of deployment use this command
               kubectl rollout history deployment nginx

               After checking history you can roll back to previous one  by using this command
               kubectl rollout undo deployment nginx --to-revision 2 


               So when you roll back your pods are now running error message will be not there

             - To delete a deployment use this command
               
               kubectl delete deploy nginx --force

               Above command will delete all depoyment pods and replicaset will be deleted nothing will be there


Statefulsets - Stateful application are those in which we have to persist the volume or store the datas.
               
             - It will create pod with predictable names even if pod dies it will recreated with same name.

             - For statefull set you have to use only headless service  

             - Headless Service - StatefulSets require a headless service to return the IPs of the associated pods and enable 
                                  direct interaction with them. The headless service has a service IP but no IP address and has
                                  to be created separately. The major components of a StatefulSet are the set itself.

             - Any service - When you use any services like you use in deployment then you can not use any replicas in case of
                              stateful apps as this  will lead to data imconsistency. 
             
             - When you delete a statefull application it will be deleted in reverse order (decreasing order) 

             some commads to check presistet volume
             kubectl get pv (persistet volume)
             kubectl get pvc (persistet volume calim)
             kubectl get sc (for storage class)

            
K8s Networking - when you  create a pod  suppose you create a 2 container pod so after pod creation CNI attach IP address and
                 attch it to network.

                 Every node has eth-0 address and his own ip address like root namespace and network namespace

                 In network namespace you will see three container 2 container which you have created and one is pause container.

                 Pause container is sleep container and it hold the network namespces
                 CNI will create a network and pause container holds the network namespace 

                 Every pod has its own ip address the CNI gives this ip address.

                 When you exec into that pod and you to type ip addr from there you will find eth-0 which is attach to root network v-eth

                 To list namespaces use this command
                 ip netns list

                 To ssh into node-1 
                 ssh node01
                 and list all namespace 

              -  To see network namespces held by   
                 pause container follow this 

                 - after exec into the pod type
                   lsns 

                   afterthat 
                   lsns |grep nginx 

                   from here you can see root network id to view it use -
                   lsns -p [root-id-num]

                   from there you can see net, uts, ipc are hold by pause container 


Service - Service helps to navigate traffic to external , internal to other port
        - Pods will come and go and pod ip will be changing every time so
          there is no any specific ip to use we need a constant ip.
          Loadbalancing when you have multiple replicas

          There are 4 types of service.

          Cluster IP
          NodePort  
          LoadaBalancer
          Headless 

          ClusterIP - This makes the service only reachable within the cluster. You cannot make requests to service (pods) from outside the cluster for that we need ingress controller

              Ingress - It is an API object that provides routing rules to manage access to the services within a Kubernetes cluster.

          NodePort - NodePort services are accessible outside the cluster. It creates a mapping of pods to its hosting node/machine on a static port.

          LoadBalancer - This service type creates load balancers in various Cloud providers like AWS, GCP, Azure, etc., to expose 
                         our application to the Internet. The Cloud provider will provide a mechanism for routing the traffic to the services. The most common example usage of this type is for a website or a web app.



        - Example of services - 
          create pod nginx -
          kubectl run nginx2 --image=nginx

        - To expose port use this command
          kubectl expose pod nginx --port 80


        - TO see the all services running
          kubectl get svc  

          from there you can see your cluster ip

        - To see the complete ip use this command
          kubectl get pods -owide  

          copy IP address and run this command
          curl [your ip-address]

          after running this command you can access your nginx locally but you can not access it from outside world.
          in order to get access you have to edit service type ClusterIP to NodePort , for that use this command 

          kubectl edit svc 
          {edit Type to NodePort}
          after that when you check svc you can see nodeport there
          kubectl get svc nginx

          Finally when you see this on nodeport you will able to see nginx welcome message 



ConfigMaps and secrets - Both ConfigMaps and secrets store the data the same way, with key/value pairs, but ConfigMaps are meant
                         for plain text data, and secrets are meant for data that you don't want anything or anyone to know about except the application.

                       - You can use environment variables in config maps.
                       - You can also use volume mount in config maps.  









 


               
 









    







                


                                         



            


        





   
