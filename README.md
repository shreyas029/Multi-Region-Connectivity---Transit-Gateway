# Multi Region Connectivity Transit-Gateway

## Description
## Architecture
## Creating VPCs
1. Log into the AWS Console and serach for 'VPC'.
2. Create a VPC with the following setting.
![ss1](https://github.com/user-attachments/assets/fc22bbb2-1f65-4165-9691-cadde125fac1)

4. Create another VPC with different with different CIDR.
![ss2](https://github.com/user-attachments/assets/3ed6fc11-3e26-4194-8810-a50e121ca10a)

5. Head over to 'Security Groups' to implement 'Inbound Traffic Rules'.
![ss2](https://github.com/user-attachments/assets/093b4e8a-a191-4ee5-ad1c-ef9919432132)

6. Repeat the same step to VPC2 as well.

## Creating Transit Gateway
1. Click on 'Create Transit Gateway'.
2. Provide a suitable name.
![tgwss](https://github.com/user-attachments/assets/3aa7cbe4-236f-4648-a855-dbba927ba881)

3. Now attach the Transit Gateway to the VPC.
![tgwvpc](https://github.com/user-attachments/assets/c7de06aa-fd7b-4d80-91ba-6452eeefa9af)

4. Since we have created 2 VPCs, attch it both. Here, VPC1 is selected.

5. And another Transit Gateway is created for VPC2.
![tgwvpc2](https://github.com/user-attachments/assets/96516dcf-2e44-45af-88ac-49f3f1b7a00b)

## Launch EC2 Instance
1. As 2 VPCs are implemented, deploy EC2 instances for each.
![ec2vpc1](https://github.com/user-attachments/assets/cce58e79-11c5-49ad-a0a7-898ceb9557de)

2. Edit the 'Network Setting' as per VPC1.
![ec2vpc1 2](https://github.com/user-attachments/assets/830b5b29-dde6-4eed-8db8-3923ce86def0)

3. Repeate the same procedure for 'VPC2'.
![ec2vpc2](https://github.com/user-attachments/assets/6eeace60-667d-44cd-9416-8f83dd736b45)

## Configure Route Table
1. Select 'VPC1' and click on 'Edit Route Table'.
2. Choose 'Add Route' and enter the IP address of 'VPC2' which was provided earlier along with Transit Gateway (TGW).
{Allow VPC2 routes in VPC1}
![rt1](https://github.com/user-attachments/assets/6f4fe25b-a521-4cc3-b5d1-1642f6dc2c44)

4. Repeat the same procedure for 'VPC2'.
![rt2](https://github.com/user-attachments/assets/f1f07354-bdac-4f3d-a223-3a4a88d3aeb8)

6. This has been implemented in North Virginia Site. Ping each instances to check the connectivity.

## Testing Connection in both Instances
Now ping the instances with each other using their Private IP address.
1. Pinging 'VPC2' from 'VPC1'.
![testconnect1](https://github.com/user-attachments/assets/bea5bec7-dc57-491a-946d-3af2e09f08e1)

2. Pinging 'VPC1' from 'VPC2'.
![testconnect2](https://github.com/user-attachments/assets/bc8eca09-9571-47a9-bc8f-1fdb0a4321c1)

## Implement the same steps in Different Availability Region
The diiferent region I have chosen is California.

1. Create an EC2 instance California Region.
![cali inst](https://github.com/user-attachments/assets/9721e7d4-23bb-46b6-98d2-c9c0fbbc7cfe)

2. Chnage the Network Setting and launch the instance.
![cali inst2](https://github.com/user-attachments/assets/a4c22938-9263-4204-b5b9-0bf0236be208)

3. Create new Transit Gateway in the new Region.
![tgwnc](https://github.com/user-attachments/assets/e77d58b1-8349-4c92-89e9-8f8603cafb5e)

4. Once the Transit Gateway is 'Available', attach this Transit Gateway to the VPC.
![attachtgwnc](https://github.com/user-attachments/assets/4e6aa2f7-28d5-489b-b6cf-e8747a9fcd7a)

5. Navigate to Route Tables and make sure to allow traffic from N.Virginia region.
![rtnc](https://github.com/user-attachments/assets/709ba0e7-0e2c-4b0b-996b-2b2a5d397538)

6. Move to N. Virginia region and add the IP address of N. California region.
![tgwnvnc](https://github.com/user-attachments/assets/00516719-5ede-495b-be7a-50bbd7c572db)

7. Send a peering request from either N.Virginia Region or N.California Region.
![peering](https://github.com/user-attachments/assets/71775405-c36c-4c3e-ba8a-0b63deec6339)

8. Accept the Peering Request from the other Region.
![reqpeer1](https://github.com/user-attachments/assets/6b5fde6c-c064-444f-a7cc-6ac29b187110)

![reqpeer2](https://github.com/user-attachments/assets/5d248967-4587-4ea3-a094-dbc2cc69da0b)

## Creating Static Routes
1. Head to N.California Region and navigate to 'Transit Gateway Route Tables'.
2. Select the 'Transit Gateway ID' and click on 'Create Static Route' and select 'Peering' option.
![static route](https://github.com/user-attachments/assets/81718a0d-605d-41b1-b00a-e27880db4318)

3. Add the IP addresses of VPCs in another Region {N.Virginia}.
4. And in the next step, add the IP address of VPC in N.California Region to 'Transit Gateway Route table' of N.Virginia Region.
5. ![static route2](https://github.com/user-attachments/assets/9a73a757-4225-48e9-923a-56aa90d0975f)

## Testing Connection 

Ping VPC in N.California from VPC1 {N.Virginia}.
![resultvpc1](https://github.com/user-attachments/assets/6aaf1fd4-62aa-41e6-8212-7584571504e7)

Ping from VPC2 {N.Virginia}.
![resultvpc2](https://github.com/user-attachments/assets/618e4d82-7fb1-482a-8e06-3136b984c4cb)









