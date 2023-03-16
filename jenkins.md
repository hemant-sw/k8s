<h1>Jenkins</h1> 
<pr>Jenkins is one of the most popular automation tool used worldwide for continuous integration and continuous delivery.
Jenkins is a free and open-source automation server that enables developers to build, integrate, and test code automatically as soon as it is committed to the source repository.</pr>

<h1>Continuous Integration</h1> 
<pr>>Continuous Integration is a process in which the code is merged from multiple contributors and added to a singlerepository.
In simple words, CI is a process to take the code package it and send it to the CD for further processing.</pr

<h1>Continuous delivery/deployment</h1> 
<pr>The basic difference between Continuous Delivery and Continuous Deployment is that in Continuous Delivery to deploy the code after the CI process you have to manually trigger it via some button to deploy on the
system whereas in Continuous Deployment this process is automatic.</pr>

<h1>Installtion process of jenkins on ubuntu</h1>

<li>Follow the official documentation of jenkins in orde to install the jenkins</li>

<li>After installtion process you have to start the jenkins on ubuntu for that follow these steps</li>

   <ul> {sudo systemctl start jenkins} this command will not produce any output.</ul>
   <ul>to check the running status of jenkins use </ul>

   <ul>{sudo systemctl status jenkins}</ul>

<li>After successfully running jenkins you can access jenkins from localhost.</li>

<li>When you open the jenkins it will ask you to unlock the jenkins for the first time for that use this command</li>
     <ul>{sudo cat /var/lib/jenkins/secrets/initialAdminPassword}</ul>  
     <ul>When you enter above command a password will be displayed on the screen copy and paste to unlock the jenkins</ul> 
     <ul>After that it will ask you to customize the jenkins and it will download some plugins.</ul> 
     <ul>When download is finshed it will ask you to create an admin account.</ul> 
     <ul>And finally jenkins is ready to use and you will be redirected to the official portal . </ul>     
<li>Setup jenkins CLI -</li><br>
     <ul>first you need to setup SSH for that use.</ul>
     <ul>Open terminal type {ssh-keygen}</ul>
     <ul>When you hit enter you get some message displayed like - Your public key has been saved in /home/hemant/.ssh/id_rsa.pub</ul>
     <ul>cat to that perticualar location and you will get you ssh key copy that entire code.</ul>
     <ul>Now go to Dashboard and click on your name on top right corner now go to config scroll to the bottom </ul>
     <ul>Now paste the entire code to the ssh public key . </ul>

<li>To access various features in Jenkins through a command-line tool</li> 
     <ul>first download jenkins-cli.jar, and run it as follows -</ul>
     <ul>After downloading the jenkins-cli.jar change directory to the particular location in the terminal and go to 
       jenkins portal and log to Dashboard/manage-jenkins/jenkins-cli </ul>
     <ul>From there copy {java -jar jenkins-cli.jar -s http://localhost:8080/ -webSocket help} and paste into terminal</ul>
     <ul>After that you get some error message that you have to authenticate your jenkins </ul>
     <ul>To authenticate follow these steps- 
        Go to Manage Jenkins -> Configure Global Security ->
        Authorization -> Logged-in Users can do anything -> Checked allow anonymous read access</ul>
     <ul>Finally run this command 
       {java -jar jenkins-cli.jar -s http://localhost:8080 -auth username:password}</ul>
     <ul>Now you can use jenkins CLI.</ul>

