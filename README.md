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


  ## Storage Gateway
  
  
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
   Origin - Is the origin off all files the the CDN will distribute. This can be either an S3 Bucket,      an EC2 Instance, AN ELB or ROute53
   Distribution - This is the name given the CDN which consists of a collection of Edge Locations.
   Web Distribution - Typically used for websites
   RTMP - Used for media streaming
     
     
     
              
   ## EC2      
   
   
   
