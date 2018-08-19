
###VPC Network Security

    You’ve been hired as a Solutions Architect by a small vacation startup, 
    Travel Salmon. They’re launching their web app in two weeks, 
    but there’s a problem 
    - your team lead recently left the company for a competitor. Before he left, 
    he set up some basic infrastructure but did not secure any of it. 
    Because the company will handle sensitive customer data, including addresses 
    and passport numbers, security is crucial.
    
    Travel Salmon’s infrastructure is contained in a single VPC called InternalVPC. 
    It is made up of eight subnets across two availability zones, divided into “layers” 
    of two subnets each. The first layer is public and contains a bastion host, 
    a NAT gateway, and an application load balancer.
     This layer is the main access point for the infrastructure. 
    
    The second layer contains the application servers, which need to communicate with a 
    MySQL database. The third layer contains admin servers, which allow employees to 
    connect to both application servers and the database for maintenance.
     Both of these layers will need to download updates, but neither should be 
     directly accessible from the internet.
    
    The fourth layer contains two EC2 instances hosting MySQL databases, 
    which should be accessible only from the application and admin servers. 
    Database admins will apply updates on an as-needed basis, so these instances 
    do not need to access the internet.
    
    Your job is to assign the correct security group to each running instance 
    (including the database and load balancer), as well as assign the proper 
    network ACLs and route tables to each subnet, based on the descriptions above.
     You should *not* use default security groups and network ACLs or the main 
     route tables as part of the final configuration. 
     Travel Salmon admins will review the security settings when you’re finished,
      so you do *not* need to make any changes to the existing networking rules.
      
      
      
#### Bastion host

     A bastion host is a secure host that accepts SSH connections only 
      from trusted sources.
     A trusted source is the static IP address of your internet connection.
     This ensures that the access to your AWS resource is from a machine 
     from within your network. 
     
     A bastion is used to administer your AWS network and instances.
     All instances accept SSH connections only from the bastion security group.
     
