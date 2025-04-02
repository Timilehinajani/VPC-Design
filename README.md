# VPC-Design
Design and set up a Virtual Private Cloud (VPC) with both public and private subnets. Implement routing, security groups, and network access control lists (NACLs) to ensure proper communication and security within the VPC.
# Creating a VPC
STEP 1: log into your AWS account
STEP 2: navigate to VPC 
STEP 3: select on create VPC 
STEP 4: setup your VPC to your specic requirments
STEP 5: select create VPC 
![Screenshot (14)](https://github.com/user-attachments/assets/dfc1622b-4c85-4170-9284-b14ca1a59847)


# Creating subnets 
STEP 1: while logged into your AWS account, navigate to subnets
STEP 2: select "create subnet"
STEP 3: select ID of created VPC
STEP 4: setup your subnet to your specifiv requirment and details for the public subnet 
STEP 5: select "add new subnet"
STEP 6: setup your subnet to your specifiv requirment and details for the private subnet 
STEP 7: select "create subnet"
![Screenshot (16)](https://github.com/user-attachments/assets/557a552d-ed59-4cb9-aaad-594672d968e4)
![Screenshot (17)](https://github.com/user-attachments/assets/910e4bc1-bd9e-4ad5-9518-c1329bae5797)


# Configuring and attaching internet gateway(IGW)
STEP 1: navigate to internet gatewaays 
STEP 2: select "create internet gateways"
STEP 3: name the IGW
STEP 4: create the IGW
STEP 5: select "attach to VPC"
![Screenshot (20)](https://github.com/user-attachments/assets/e4a3f118-c11b-4764-976b-68e4c8d6f6db)


# configuring route tables
STEP 1: navigate to route tables
STEP 2: select "create route tables"
STEP 3: name the route for public subnets and select the VPC
STEP 4: select "create route tables"
STEP 5: select "create route tables"
STEP 6: name the route for private subnets and select the VPC
STEP 7: select "create route tables"
![Screenshot (23)](https://github.com/user-attachments/assets/30b67d4d-2160-4950-b82c-ee48d8955487)


# Associating subnet with route table
## Public route table
STEP 1: select public route table
STEP 2: select "actions" drop down
STEP 3: select "edit subnet associations"
STEP 4: select the publicsubnet
STEP 5: select "save associations"
STEP 6: select public route table
STEP 7: select "edit route"
STEP 8: select "add route"
STEP 9: input destination as 0.0.0.0/0
STEP 10: input target as the internet gateway vreated 
## Private route table
STEP 1: select private route table
STEP 2: select "actions" drop down
STEP 3: select "edit subnet associations"
STEP 4: select the privatesubnetct
srep 5: select "save associations"
![Screenshot (26)](https://github.com/user-attachments/assets/b3b19838-c8e7-4de1-88e4-7e94f057e81a)


# Configuring NAT gateways
STEP 1: select "NAT gateway"
STEP 2: select "create NAT gateway"
STEP 3: setup your NAT gateway and allocate ellastic IP
STEP 4: select "create NAT gateway"
STEP 5: navigate to route table 
STEP 6: select private route table
STEP 7: select "actions" drop down
STEP 8: select "edit route"
STEP 9: edit destination to 0.0.0.0/0 and target to the NAT gateways just created
STEP 10: select "save changes"
![Screenshot (25)](https://github.com/user-attachments/assets/ac80e87b-2a9e-4d25-83d3-741381609b82)

NOTE: The reason for creating NAT gateway is so that if you are in your private instance and you want to access the internet its going to go through our NAT gateway

# creating security group
STEP 1: navigate to security group
STEP 2: select "create security group"
STEP 3: setup your security group with the appropriate imbound and outbound rules
STEP 4: select "create security group"
![Screenshot (27)](https://github.com/user-attachments/assets/dca88f76-fd33-44b2-b601-a5230255d31c)
![Screenshot (28)](https://github.com/user-attachments/assets/e402cb58-4795-4c07-88bd-1c9442455516)
![Screenshot (29)](https://github.com/user-attachments/assets/20e66c73-ff5e-4c71-9f98-322b799d9687)

# Deploy Instances
## Public
STEP 1: navigate to EC2 and launch instance 
STEP 2: setup instance with previously created VPC, public subnet and public security group
STEP 3: select "launch instance"
![Screenshot (31)](https://github.com/user-attachments/assets/32d4a430-bf04-4f25-b32e-e4a53a0b0242)


## Private
STEP 1: launch another instance 
STEP 2: setup instance with previously created VPC, private subnet and private security group
STEP 3: select "launch instance"
![Screenshot (32)](https://github.com/user-attachments/assets/30445584-876d-4898-b191-5062424b6185)

# BREIF EXPLANATION 
## Virtual Private Cloud (VPC):
The VPC is a logically isolated network within the cloud where you can launch AWS resources securely. It enables control over IP address ranges, subnets, route tables, and network gateways, providing a customizable environment.

## Subnets (Public and Private):

Public Subnet: Allows resources, such as web servers, to be accessible from the internet. It has a route to the Internet Gateway (IGW).

Private Subnet: Hosts internal resources (e.g., databases) that don’t require direct internet access. It routes outbound traffic through a NAT Gateway for internet access.

## Internet Gateway (IGW):
The IGW enables communication between the VPC and the internet. It allows inbound and outbound traffic to resources in the public subnet.

## NAT Gateway:
The NAT Gateway allows instances in the private subnet to initiate outbound internet traffic (e.g., software updates) while preventing inbound traffic from the internet.

## Route Tables:
Route tables define how network traffic is directed within the VPC:

The public route table routes internet-bound traffic from the public subnet to the IGW.

The private route table routes internet-bound traffic from the private subnet through the NAT Gateway.

## Security Groups:
Security Groups act as virtual firewalls for instances, controlling inbound and outbound traffic at the instance level. They operate on a stateful basis, meaning responses to allowed traffic are automatically permitted.

## Network Access Control Lists (NACLs):
NACLs are stateless firewalls controlling inbound and outbound traffic at the subnet level. They provide an additional layer of security by allowing or denying traffic based on IP addresses and port ranges. Unlike security groups, NACLs require explicit rules for return traffic.
