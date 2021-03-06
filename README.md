# AWS SAA-Notes
  
  ## Quick Notes
Project is created with:
* EC2 exposes a standard Linux machine we can use any way we want
* RDS expose a standard database we can connect using a URL
* ElastiCache exposes a cache URL we can connect to using a URL
* ASG/ELB are automated and we don't have to program against them
* Route 53 was setup manual

## CLI (Command Line Interface) 



   ## S3 

 * Snowball is good when you want to transfer/migrate data to AWS. Can scale in Petabytes
 * Snowball comes in 50TB or 80TB
 * Snoball Edge is data transfer device with compute cabalities comes in 100TB or to support workload in remote or offline locations
 * Snowmobile is when you want to transer/migrate Exabyte-scale data. You can transfer up to 100PB per snowmobile
 * Snowball can import/export to S3 


  ### Storage Gateway
  
  
  * Is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration beetwenn an on-premise devise to AWS's storage infrastructure 
  * Securely store data to the AWS cloud.
  * Is available as a VM that you install on host in your datacenter.
  * Supports either Microsoft Hyper-V or VMware ESXi
  * After installation you can use the Management Console to create the storage gateway option.
  * Three different types of Storage:
          * File Gateway (NFS & SMB)
          * Volume Gateway (iSCSI)
                Stored Volumes 
                Cached Voumes
          * Tape Gateway (VTL)
          
   * In a nutshell is a way to connect your on-premise infrastructure to S3
   * The volume interface presents your applications with disk volumes using the iSCSI block protocol
   * Data written can be asynchronously backed up as snapshots of your volumes and stored as EBS volumes
   * You can store your data locally with stored volumes. 
   * With Cached volumes you can only store the frequently accessed data locally 
   
   * File Gateway - For flat files, stored directly on S3
   * Volume Gateway - 
          Stored Volumes - Entire Datased is stored on site and asynchronously backuped to to s3
          Cached Volumes - Entire Datased is stored on S3 and the most grequnetly access data is cached on site
          Gateway Virtual Tape Library
            Used for backup and uses popular backup applications like NetBackup Exec, Veeam etc
          
   ## Athena
   
   * Enables to analyze and query data located in S3 using standard SQL.
   * Serverless, nothing to provision, pay per query / per TB scanned
   * No nned to set up complex Extract/Transform processes
   * Works directly with data stored in S3
   
   * Can be used: 
          Query log files stored in S3
          Generate business reports on data stored in S3
          Analyse AWS Cost and usage reports
          Run queries on click-stream data
          
          
  ## Macie
   
   * Is a security service which uses Machine Learning and NLP (Natural Language Processing) to discover, classify and protect sensitive data store in 
     S3.
   * Uses AI to recognise if your S3 objects contain sensitive data such as PII
   * Dashboards, reporting and alerts
   * Works directly with data stored in S3
   * Can analyse CloudTrail logs
   * Great for PCI-DDS (Card payments) and preventing ID theft
   
  
   * Tips:
        Athena is an intractive query service
        It allows you to query data located in S3 using standard SQL
        Serverless
        Commonly used to analyse log data stored in S3
        
        Macie uses AI to analyse data in S3 and helps identify PII
        Can be used to analyse CloudTrail logs for suspicious API activity
        Includes Dashboards, Reports and Alerting
        
        
        
        
   * S3 Tips
    
   Read after Write consistency for PUTS of new objects
   Eventual Consistency for overwirte PUTS and DELETES (can take soem time to propagate) 
    
   Three different ways to share S3 buckets across accounts
    
   Using Bucket Policies & IAM (applies acrros the entire bucket).
   Programmatic Access Only
      
   Using Bucket ACLs & IAM (individual objects). Programmatic Access Only
      
   CRR
      
   Files in an excisting bucket are not replicated automatically
   All subsequemnt update files will be replicated automatically
   Delete Markers are not replicated
   Deleting individual versions or delete markers will not be replicated
      
      
      
   S3 Transfer accelaration uses edge locations to improve transfer
      
     
   CloudFront
   Origin - Is the origin off all files the the CDN will distribute. This can be either an S3 Bucket,      an EC2 Instance, AN ELB or Route53
   Distribution - This is the name given the CDN which consists of a collection of Edge Locations.
   Web Distribution - Typically used for websites
   RTMP - Used for media streaming
     
     
     
              
   ## EC2      
   
   
   ### EBS
   
   * Provides persistent block storage volumes for use with EC2
   * Each EBS volume is automatically replicated within its AZ to protect from component failure, 
   * High availability and durability
   * Different Types of EBS
       * General Purpose SSD (gp2) Most work loads (MAX IOPS/Volume - 16000)
         Balances price and performance for a wide variety of transactional workloads
         
       * Provisioned IOPS SSD (io1) when you want really, really fast IOPS Databases (MAX IOPS/Volume - 64000)
         Highest performance SSD designed for mission-critical applications
         
       * Throughput optimised HDD (st1) Big Data & Data Warehouses (MAX IOPS/Volume - 500)
         Low cost HDD volume for frequently accessed, through-put intensive workloads
         
        * Cold HDD (sc1) File serves (MAX IOPS/Volume - 250)
          Lowest cost HDD volume designed for less frequenly accessed workloads
          
        * EBS Magnetic (Standard) Workloads where data is IA (MAX IOPS/Volume 40-200)
          Previous generation HDD
          
       *  When you modify the size of the volume and increase it in size you have to go inside the EC2 and               repartition the hard drive.
       
       
       All AMIs are categorized as either backed by Amazon EBS or backed by an instance store.
       
       
       For EBS Volumes: The root device for an instance launched from the AMI is an Amazon EBS volume created   
       from an Amazon EBS snapshot.
       
       For Instance Store Volumes: The root device for an instance launched from the AMI is an instance store 
       volume created from a template stored in Amazon S3
       
       Instance Store Volumes are sometimes called Ephmeral Storage. They cannot be stoped. IF the underlying          host fails, data will be lost.
       
       EBS backed instances can be stopeed. You will not lose the on this instance if it is stopped.
       
       You can rebbot both, you will not lose your data.
       
       By default both ROOT volumes will be deleted on termination. However, with EBS voluems you can tell AWS        to keep the root device volume.
      
      
      
     ## ENI ENA EFA
      
      
       * ENI (ELastic Network Interface) - essentially a virtual card
       
       * EN Enchanced Networking. Uses single root I/O virtualisation 
        (SR-IO~V) to provide high-performance networking capabiliteis on supported instance types.
        
       * Elastic Fabric Adapter A network device that you can attach to your EC2 to accelerate 
         High Performance Computing (HPC) and machine learning applications
         
         
        ENI allows :
                     A Primary private IPv$ address from the IPv4 address range to your PC
                     One or more seconday private IPv4 addresses from teh IPv4 address range to your PC
                     One Elastic IP address (IPv4) per private IPv4 address
                     One public IPv4 address
                     One or more IPv6 addresses
                     One or more security groups
                     A MAC address
                     A source/destination check flag
                     A description
                  
        Scenarios for Network Interfaces:
                     Create a management network
                     Use netwrok and security appliances in your VPC
                     Create dual-homes instnaces wtih workloads/roles omn disting subnets.
                     Create a low-budget, high-availability solution
                     
                    
                    
        When ENI is not enough EN comes to help
          
        It uses signle root I/O virtualization (SR-IOV) to provide high-performance networking capabilities to         supported instance types . SR-IOV is a method of device virtualization that provides higher I/O
        performance and lower CPU utilisation when compared to traditional virtualized network interfaces. 
        Vroom Vroom 
        
        
        Enchaned networking provies higher bandwith, higher packet per second (PPS)
        performance, consistenly lower inter-instance latencies. THere is ot additional charge for using 
        enchanced networking. 
        
        Not all instances support
        
        Use when you want good network performance
         
        
        
        
        Depending on your instance type, EN can be enabled using:
        
        Elastic Network Adapter (ENA), which support network speeds of up to 100 GBps for supported instance 
        types
        
        Or
        
        Intel 82599 Virtual FUnction (VF) interface, which supports network speeds of up to 10 Gbps for 
        supported instance types.
        This is typically used on older instances.
        
        In any scenario question, you probably want to choose ENA over VF of given the option
        
        
        
        EFA (Elastic Fabric Adapter) is a network device that you can attach to your EC2 instance to accelerate 
        HPC and ML applications
        
        ELA provides lower and more consistent latency and higher throuput than hte TCP transport
        traditionally used in cloud-based HPC systems?
        
        
        EFA can use OS-bypass. OS-bypass enables HPC and ML applications to bypass the operating system kernel 
        and to communicate directly with EFA device. It makes it a lot faster with a lot lower latency. Not 
        supported with Windows currrently, only LInux.
        
        
        ENI 
          For basic networking. Perhaps you need a separate management network to your production networm or a 
          parate logging network and you neet to do this at lowcost. In this scenario use multiple ENIs for 
          each network.
          
        EN
          For when you need sppeds between 10Gbps and 100Gbps. Anywhere you need reliable, highi throuput.
          
        EFA
          For when you need to accelerate HPC and ML applications or you need to an OS by-pass. If you see a 
          scenario question mentionting HPC or ML and asking what network adaptor you want, choose EFA.
          
          
          
        Encrypted Rood Deice Volumes & SNapshots - LAB
        
        Provision EC2 - Take snapshot, make copy of snapshots - when you make copy then encrypt. Then create an
        image from snapshot, creates encrypted AMI which we can use to launch encrypted EC2
        
       
        
        You can now encrypt when you provision EC2
      
        You cannot take an encrpyted snapshot image to make EC2 and then choose to unencrtypt while on the 
        storage page of EC2
        
        You share snapshots but only if they are unencrypted 
        
        
        
        Spot Instances
        
        If the price goes above the want you set. You have 2 minutes do decide if you want to keep the instance         or not
        
        You may also use Spto Block to stop the instance even if it gets terminated even if the Spot price goes 
        over the one you set. You can set Spot Block from from 1 to 6 hours currently
        
        
        Spot Instances are good for:
              Big data and analytics
              Containers workload
              CI/CD and testing
              Web services
              Image and media rendering
              HPC
              
              
        Not got for:
            Persistent workloads
            Critical jobs
            Databases
       
       
       Spot Request Types:
          One Time, Persistent, Valid from, Valid until
          
          
          
       Spot Fleets a colleciton of Spot Instances and Optionally on Demand Instances
       
       You can set up launch pools. Define EC2's OS, AZs
       
       You can have multiple pools and the fleet will choose the best way to implement depending on the     
       strategy you define
       
       Spot Fleets will spot launching instances when you reach the your price threshold or capacity desire.
       
       
       
       Strategies that you have with Spot Fleets
       
       capacityOptimized: The Spot Instances comes from the pool with optimal capacity for the number of 
       instances launching.
       
       lowestPrice:  The Spot instacnes come from the pool with the lowest price. THis is the default strategy
       
       diversified:  The Spot instances are distributed accress all polls
       
       
       InstancePoolsToUseCount:  The Spot instances are distributed across the number of Spots Instance pools 
       you specify. This parameter is valid only with when used in combination with lowestPrice.
       
       
       
       In a nutshell :
                      Spot Instaces save up to 90% of the On-Demand Instances.
                      Usefiul for any type of computing where you don't need persistent storage.
                      You can block Spot Instances from terminating by using Spot Block
                      A Spot Fleet is a collection of Spot Instances and, optionally, On-Demand Instances.
                      
                      
       
       
       EC2 Hibernate : When you hibernate an EC2 instance, the OS is told to perform suspend-to-disk. It will 
       save the contents from Instance memory (RAM) to your EBS root volume. We persist the Instance's EBS root
       root volume and any attached EBS data volumes
       
       When you start again out of Hibernation:
          THe EBS root volume is restored to its previous state.
          The RAM contents are reloaded
          The processses that were previously running on the instance are resumed.
          Previously attached data volumes are reattached and instance retains its instance ID
       
       Much faster to book as you dont need to reload the OS
       Instance RAM must be less than 150GB
       Available for Windows, Amazon Linux 2, and Ubuntu
       Instance  include C3, C4, C5, M3, M4, M5, R3, R4, and R5
       No more than 60 hibernation
       Available for On-Demand and Reserved
       
       
       
       CloudWatch
       
       With CloudWatch you can monitor your resources and the applications that you run on AWS.
       CloudWatch is to monitor performance.
       
       
       You can Monitor on EC2 Host Level Metrics
       CPU 
       Network
       Disk
       Status Check
       Underlying hypervisor
       
       CloudWatch on EC2 will monitor by default
       You can have 1 minute intervals by turning detailed monitoring.
       You can create alarms which trigger notifications.
       CloudTrail is for auditing.
       
       Standard monitoring is 5 min expited is 1 min
       Create dashboard to see what is happening with your environment.
       You can set Alarm to notify you when  partucular thresholds are hit.
       CW events helps you to respond to stage changes in your resources.
       CW logs helps you to aggregate, monitor and store logs.
       
       
       Roles are more secure than storing your access key and and secret access key on individual EC2 
       instances.
       Easier to manage.
       Roles can be assigned to an instance after its created using the console and command line.
       
       
       ### Meta-Data / User-Data
       
       curl http://169.254.169.254/latest/ meta-data/ or user-data/
       Meta-data for getting information such as IP
       User-data for getting information such as bootscrapt script
       
       
       
       ## EFS
       
       Elastic File System is is a storage service for EC2.
       Easy to use and provides a simple interface that allows you to create and configure file systems
       easily and quickly.
       Storage capacity is Elastic meaning is growning and shriking automatically as you add and remove files.
       You applications can have the storage they need, when they need it.
       Good for sharing files between EC2's
       When use it don't forget to set inbound rules.
       
       
       Supports the NFSv4 protocol
       You only pay for the storage you use
       Can scale up to petabyets
       Can support thousands of concurrent NFS connections
       Data is stored accroiss multiple AZ's within a region
       Read After White Consistency 
       
       
       
       ### FSx for Windows / FSx for Luster
       
       
       FSx for Windows File Server provides a fully managed native Microsoft file system so you can easyli
       move your Windows-based applications that require file storage to AWS. FSx is build on Windows Server.
       
       Windows FSx vs EFS
       
       Windows FSx
       -When you need centralised storage for Windows based apps such as Sharepoint, Microsoft SQL,
        Workspaces, IIS Web Server or any other native Microsoft app
       -Runs Windows Server Message Block (SMB) based file services.
       -Designed for Windows and Windows Applications
       -Supports AD users, access control lists, groups and security polices, along with 
       DFS namespaces and replication.
       
       
       EFS
       
       - A managed NAS files for EC2 instances based on NFSystem v4
       - One of the first network file sharing protocols native to Unix and Linux
       - When you need distributed, highly resilient storage for Linux instanceds and Linux-based applications.
       
       
       
       Placement Groups 
       
       Cluster 
          Is a group of instances in a single AZ. 
          Good for Low network latency, high network throughput, or both.
          Only certain instances can be launched in Cluster
          
          
      Spread Placement
          Is a group of instances that are each placed on underlying hardware.
          IndivIDUAL Critical EC2 instances
          Good for apps that have small number of critical instances that need/should be kept seperated from
          each other
          You can have seperate groups in different AZs with in one region.
          Designed to protect from hardware failure.
          
          
      Partitioned Placement
          Is a group of instances that EC2 divides each group into logical segments called partitions.
          EC2 ensures that each partition within a placement group has its own set of racks.
          Multiple EC2 instances HDFS, HBase and Cassandra
          Each rack has its own network and power source.
          No two partitions within a Placement group share the same racks,
          allowing you to isolate the impact of hardware failure within your application.
          
       
       
       FSx Lustre
       - Is a fully managed file system that is optimized for compute-intensive workloads, such as high-   
       performance computing, ML, media data processing workflows, and electronics design automation (EDA)
       
       - With FSx you can run a Lustre file system that can process/read-write massive data sets at up to 
       hundres of gigabytes per second of throughput, millions of IOPS, and sub-millisecond latencies. 
       - Can store directly data on S3.
       
       
       HPC with AWS
       HPC is used for indristries such as genomics, finance and financial risk modeling, machone learning
       weather prediction, autonomous driving.
       
       Data transfer, Compute and Networking, Storage, Orchestrations and automation are different services we 
       can use to achieve HPC.
       
       Data transfer
       Snowball, Snowmobile. 
       AWS DataSync to store on S3, EFS, FSx for Windows.
       DirectConnect
       
       Compute and Networking Services that allow you to achive HPC
       
       EC2 instances that are GPU or CPU optimised
       EC2 Fleets (Spot Instances or Spot Fleets)
       Placement groups (cluster placement groups)
       Enchaned Networking
       Elastic Network Adapters
       Elastic Fabric Adapters
       
       EN 
        Uses single root I/O virtualization (SR-IOV) to provide high-performance networking capabilities on 
        on supported instace types. SR-IOV is a method of device virtualization that provides higher I/O
        performance and lower CPU utilization when compared to traditional virtualized network interfaces.
        
        EN
        Provides higher bandwith, higher packet per second (PPS) and consinstency lower inter-instance 
        latencies. There is no additional networking.
        
        Use where you want good network performance.
        
        Depends on instnace EN can be enabled:
                      Elastic Network Adapter (ENA), whichi supports network speeds of up to 100Gbps for 
                      for supported instance types.
                      
                      Intel 82599 Virtual Function (VF) interface, supports network speeds up to 10 Gbps. This 
                      is used mainly on older instances.
                      
                      If you have the option is probably best to use ENA over Intel VF
       
       
       
       
       Elastic Fabric Adapter (EFA) is a network device you can attach to your EC2 Instance to accelerate HPC
       and ML applications
       Provides low, more consistenct latency and higher throuput than the TCP transport traditionally use on 
       cloud-based HPC Systems
       Can use OS-bypass, which enables HPC and ML applications to bypass the OS Kernel and communicate 
       directly with the EFA device. It makes it alot faster with much lower latency. It is not supported with
       Windows only Linux.
       
       
       
       Storage services for HPC
       
       
       EBS: Scale up to 64k IOPS with Provisioned IOPS (PIOPS)
       Instance Store: Scale to millions of IOPS; low latency.
       
       
       Network storage
       S3
       EFS
       FSx for Lustre
       
       
       
       Orchestration & Automation for HPC
       
       
       AWS Batch enables developoers, scientics and engineers to easily and efficiently run hundreds of 
       thousands of batch computing jobs on AWS.
       Supports multi-node parallel jobs, which allows you to run a single jon that spans multiple instances.
       You can schedule jobs and launch EC2 instances according to your needs.
       
       
       ParallerCluster
       Open-source cluster management tool that makes it easy for you to deploy and manage HPC clusters on AWS
       Uses a simple text file to model and provision all the resources needed for your HPC applications in an 
       in an automated seccure maneed.
       Automate creation of VPC, subnet, cluster type, and instance type.
       
       
       
       AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that 
       are forwaded to CLoudFront an Application Load Balancer or API Gateway.
       Lets you control access to your content. Is a level 7 layer protocol
       More to add.
       
       
       
      
