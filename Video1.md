Introduction
In this lab, we will go through the process of creating and configuring a new Virtual Private Cloud (VPC). Along the way, we will create a couple of subnets and an internet gateway, plus learn about the differences between public and private subnets.

Create a VPC
Let's start by creating a new Virtual Private Cloud (VPC).

Navigate to the VPC Dashboard in AWS.
Click the Your VPCs link in the navigation pane to the left of the page.
Click the Create VPC button at the top of the list.
Set the Name tag to my-new-vpc
Define the IPv4 CIDR block to be 10.0.0.0/16
Leave the IPv6 CIDR block and Tenancy settings unchanged.
Click the Yes, Create button.
You will see the new VPC named my-new-vpc in the list of VPCs. We can move on to configuring subnets.

Configuring subnets
We will create two subnets: a private and a public. Let's quickly discuss the difference before moving on.

Private Subnets vs. Public Subnets
A private subnet is one without an internet gateway and is therefore "isolated" to our VPC. A public subnet is one that does have an internet gateway attached, allowing it to interact with the outside world. New subnets are created without internet gateways attached and are therefore initially private. If you intend to create a public subnet, you'll have to attach an internet gateway. This lab demonstrates such a process.

Create new subnets
We will now create two new subnets. We want one to be public and one to be private, so we will need to create and attach an internet gateway to one of them. Let's start by creating the subnet we want to be private.

Click the Subnets link on the left of the page.
Use the Create Subnet button to get started.
Since this is a subnet we intend to keep as private, type a Name tag of my-private-subnet.
Set the VPC to the new one we created (identified by the my-new-subnet name we gave it).
For the Availability Zone, we can choose us-east-1a. If you don't see us-east-1a, just choose another option and it will work the same way.
Set the IPv4 CIDR block to 10.0.1.0/24
Click the Yes, Create button.
Now we will create the subnet we want to be public.

Click the Create Subnet button.
Set the Name tag to my-public-subnet so that we can easily identify which subnet we intend to be public (we will attach the Internet Gateway to this one later in the lab).
Set the VPC to my-new-vpc
Choose the same availability zone as the private subnet: us-east-1a
Set the IPv4 CIDR block to 10.0.2.0/24
Click Yes, Create
We will see both subnets listed on the page. Now we need to make the subnet we just created (my-public-subnet) public by creating and attaching an Internet Gateway.

Create Internet Gateway
Let's create an Internet Gateway that we can attach to our VPC in order to be able to create public subnets.

Click the Internet Gateways link on the left of the page.
Click the Create Internet Gateway button
Type a Name tag of my-internet-gateway to fit the naming convention we've used in the lab so far.
Use the Yes, Create button to create the Internet Gateway.
You will see the new Internet Gateway listed on this page. Notice that it's State is detached. Attach it to the VPC we created:

Right click the my-internet-gateway listing and choose the Attach to VPC option.
Select the my-new-vpc option.
Click Yes, Attach
The State will now show attached.

Attaching the Internet Gateway with a Route Table
We will now configure a new Route Table for the Internet Gateway and explicitly associate it to the subnet we want to be public.

Navigate to the Route Tables page.
Click the Create Route Table button.
Type a Name tag of my-route-table
Set the VPC to my-new-vpc.
Click the Yes, Create button.
You'll see the new Route Table in the list. It should be selected by default. We'll configure it further using the pane at the bottom of the page.

Let's add a new route for the Internet Gateway:

Click the Routes tab.
Click the Edit button.
Click the Add another route button to add an entry.
For the Destination, type 0.0.0.0/0 (this represents any/every IP address).
For the Target, select the Internet Gateway we created a moment ago (we named it my-internet-gateway).
Click the Save button.
We can now explicitly associate this Route Table to the subnet we want to be public:

Navigate to the Subnet Associations tab.
Click the Edit button.
Check the Associate box beside the subnet we called my-public-subnet
Click the Save button.
Since we've connected an internet gateway, the subnet we called my-public-subnet is now actually public.

We have completed all of the tasks for this lab.