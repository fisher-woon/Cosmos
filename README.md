# Cosmos
Step by Step Setup Cosmos and Nginx using AWS VPC with Public Subnet and Private Subnet

# Create Elastic IP
1) Login to your AWS Account
2) In the navigation pane, click **Elastic IPs**
3) Click **Allocate new address**, then click **Allocate**

# Create and Configure Your VPC
### Create a New VPC
1) Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
2) In the navigation pane, click **VPC Dashboard**. If you do not already have any VPC resources, locate the Your Virtual Private Cloud area of the dashboard and click Get started creating a VPC. Otherwise, click **Start VPC Wizard**. 
3) Select the second option, **VPC with Public and Private Subnets**, and then click **Select**. 
4) Update **VPC Name** and **Available Zone** choose us-east-2c and **Private subnet name** enter Public Subnet **Elastic IP Allocation ID** choose Elastic IP that generate at above step, the rest remain default.
5) Click **Create VPC**, It takes several minutes for the VPC to be created. After the VPC is created, proceed to the following section to add a second subnet

### Add a Second Subnet
1) Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
2) In the navigation pane, select **Subnets**, select **Create subnet**.
3) Update **Name tag** as Private Subnet and **VPC** choose vpc that created early and **Availability Zone** choose us-east-2a and **IPv4 CIDR block** enter 10.0.1.0/24, then click **Create**
