# AWS_JumpBox

## Prerequisites

### Create a Virtual Private Cloud (VPC)
Select "Create VPC" in Your VPCs. I called my VPC ```"Fouad_A19"``` with an IP v4 : ```10.0.0.0/16``` 

### Create a public and a private subnet
We then create a public subnet  and an internet gateway to connect the VPC to the internet. Then add the internet gateway created to the route table. One route table for one subnet.
