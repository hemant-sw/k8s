what is AWS ? 
Amazon Web Services (AWS) is the world's most comprehensive and broadly adopted cloud, offering over 200 fully featured services from data centers globally.

What is IAM ( identity and access managaer) 
 - IAM allows you to manage users and their level of access to the aws console.
   IAM identities 
   - IAM identities are created to provide authentication for people and processes in your aws account.
   There are three IAM identities.
   - IAM Users
   - IAM Groups
   - IAM Roles


IAM users 
- An IAM User is an entity created in AWS that provides a way to interact with AWS resources.
  
  How to create IAM users 
  - Sign in to the AWS Management Console.
  - Open the IAM Console at https://console.aws.amazon.com/iam/home?region=us-east-2#/home.
  - On the navigation pane, click on the Users. After clicking on the Users.
  - Click on the Add User to add new users to your account. After clicking on the Add User.
  - Enter the User name for the user you want to create. You can create five users at a time.
  - Select Provide user access to the AWS Management Console.
  - And choose i want to create an IAM users and select custom passoword
  - On set permisssion options select attach policies directly
  - On users group attach desired policies
  - Finally review all information and create usres
  - To login you have to provide account id & alias , IAM username and password that's it , Done.




How to create virtual machine on aws ?

- We can create with the help of EC2
  EC2 stands for Amazon Elastic Compute Cloud.
  Amazon EC2 is a web service that provides resizable compute capacity in the cloud.
  Amazon EC2 reduces the time required to obtain and boot new user instances to minutes rather than in older days, if you need a server then you had to put a purchase order, and cabling is done to get a new server which is a very time-consuming process. Now, Amazon has provided an EC2 which is a virtual machine in the cloud that completely changes the industry.
  You can scale the compute capacity up and down as per the computing requirement changes.

- Navigate to aws EC2
- Click on Instances
- then click on launch instances give it a name and select OS image
- Choose free tier 

- Key pair ( used to login to your virtual machine)
  - click on create key pair
  - give key pair a name and click on create key pair
  - Your key pair will be saved in the downloads as pem file ( important).


- And finally  launch instances and your virtual machine is created after few minute when you see to your instances dashboard it will be on running state. 

How to connect to the aws ubuntu instance from your terminal ?

- SSH to the location where you store your .pem file
   <chmod 600 /Users/Device_name/Downloads/pemfile>
   <ssh -i /Users/Device_name/Downloads/pemfile ubuntu@Your_public_ip_adderess>

   After that you will be successfully logged into the AWS instances
   - First update your ubuntu machine
     <sudo apt update>
   - use Bash because it is widely use 
     <sudo apt install bash>
   - After that install aws cli 
     <sudo apt install awscli>
   - Installing aws cli will not do any thing because you have just installed aws cli binary and that binary has no data of our   
     user information so you have to authenticate your aws for that
   - Go to your aws console
   - Click on user option in top right most corner
   - Select security credential 
   - In access key click on create access key and your access key and private access key will be generated
   - After that go to your cli 
     <aws configure > 
     It will ask you to enter access key and secret access keys and you will be authenticate with aws cli  


How to deploy your project on AWS EC2

- Create an EC2 instance
- Connect to the aws ubuntu instance from your terminal
- install all the neccessary thing in order to run the application like nodejs npm
- clone the repo
- Now cd to the cloned repo and run <npm install> 
- finally run <npm run start> and development server will be started
- But when you run the app on your ubuntu IP address it will not run because for that you need to 
set traffic rules 
- Go to EC2 instances and Select instance in bottom you will see a security option and click on security group
- here you see inbound rules , click on edit inbound rules
- Click on edit rules and set port range 3000 and select source as anywhere

