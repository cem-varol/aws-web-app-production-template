# aws-production-configuration-template-for-web-applications

TOPOLOGY 


Create VPC 

- 2 availability zones
- 2 public subnets
- 2 private subnets
- 2 NAT geteways
- 1 internet gateway 

Create a launch template
- select AMI image (Ubuntu 24.0)
- Select instance type(t2.micro)
- provide key-pair for authentication	
- In network settings choose previously ceated VPC 
- Add security group: add inbound security rules for ssh and http

Create auto scaling group for EC2 instances
- Select previously created launch template
- Select previously created VPC
- Select availability zones 
- Select the PRIVATE subnets in this VPC, in both AZs.
- Follow the wizard and chooose minumum desired capacity 2, maximum desired capacity 4
- Than click create
- Check the status of EC2 instances (created or not)


Create a target group for High Avalability 

- Click create target group 
- Chooose the VPC
- Select the EC2 instances and than click to register targets (the EC2 instances previously created)
- Click create target group 
  

Create a Load Balancer

- In AWS console earch Load Balancer and navigate to the Laod Balancers page
- Click create load balancer 
- Select application loadbalancer
- Choose IP4 and internet facing option 
- In network mapping section choose your VPC and availability zones
- Under availbility zones choose your PUBLIC subnets
- choose your security group for EC2 intances
- choose your target group in Listeners and routing section 
- Leave other options as default and click "create load balancer"
 
Deploy youe Web Appliction to EC2 Instances: 

- create a jump host in public subnet area(public-subnet in one of the AZs) in the topology
- choose your VPC.
- choose the publix subnet
- Assign a public IP address to jump server.
- Add ssh connection rule to security group for EC2 instance
- Make an ssh connection to this instance with public IP 
- Upload your aws-key to this instance with scp command
- Make an ssh connection(with the key copied to this insatnce) to one of the instances in private subnet area(private subnet in one the AZs)   
- Deploy your application 
- Repeat same procedure for other instance.


Check the Load Balancing, HA behaviours

- If you can obeserve round-robin request diretion to each instance, you are done... 
