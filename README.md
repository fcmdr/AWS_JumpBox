# AWS_JumpBox

## Create a Virtual Private Cloud (VPC)
Select "Create VPC" in Your VPCs. I called my VPC ```"Fouad_A19"``` with an IP v4 address : ```10.0.0.0/16``` 


## Launch 3 instances

### Public instances

-Launch an NAT instance, in EC2 select in ```AMI community amzn-ami-vpc-nat```
enable public IP (it is also possible to allocate an elastic IP), select the VPC we created, we keep the default storage.
Name the instance : ```NAT INSTANCE``` for example
Create a security group and give it a name  ```SG_NAT_Instance``` (In inbound and outbound rule accept connections from the private subnet IP v4 : 10.0.100.0/24). Create a key pair as we should have 1 key pair per machine.

-Create a JumpBox instance : Select a free tier machine, associate it to the VPC, enable a public IP, create a key pair. Give a name to the JumpBox instance ```JumpBox```, and associate it to a security group ```SG_JumpBox```

## Create public and private subnet 

-Create a public subnet and attach it to our VPC, put an IP v4 address : ```10.0.1.0/24```.
Route table click on route table itself in route table (in left we will be in route table)
Select internet gateway and allow access to every IP address.

-For the private subnet : In create subnet,select our VPC, put an IP v4 address for example : ```10.0.2.0/24```.
Do not associate the private subnet to the internet gateway.
Create a public route table associated with the VPC and an internet gateway.
***Very important ! Create a private route table (different from the public route table) associated with the VPC and the NAT Instance (not to the internet gateway).***

![image](https://user-images.githubusercontent.com/58029143/69902903-11531800-1393-11ea-9c0f-ffc3004855a5.png)

### Private instance

-Private instance : Let's call it ```Final Instance```, we must disable public IP we put instance in private subnet then we create another key pair associated to the instance. Accept inbound connection from the security group of the JumpBox via SSH. 

## Connection to the private instance via the JumpBox

Put key on JumpBox instance :
``scp -i "C:\Users\Fouad\Desktop\DSTI courses\AWS\FI_KeyPair.pem" "C:\Users\Fouad\Desktop\DSTI courses\AWS\FI_KeyPair.pem" ec2-user@"JumpBox IP":~``

Let permissions : ```chmod 0600 FI_KeyPair.pem```
Connection to the private instance : ```ssh -i FI_KeyPair.pem ec2-user@"Final Instance's IP"``` and ping google.com !

## Result 

![image](https://user-images.githubusercontent.com/58029143/69903155-60e71300-1396-11ea-82f9-385c42d53f96.png)





