# aws-solution-architecture-professional-note

## Cost Management 
- Compute Optimizer creates a dashboard shows you savings and performance improvement opportunities at the account level.
  - Only works with EC2, Lambda and EBS
 
## Global Infrastructure
- Global Accelerator can only be placed in front of Load Balancers, not CloudFront Distribuitions.
  - Global Accelerator provides two global static public IPs that act as a fixed entry point to your application endpoints, such as Application Load Balancers, Network Load Balancers, Amazon Elastic Compute Cloud (EC2) instances, and elastic IPs.

 ## Disater Recovery
 - Elastic Disater Recovery create a minimal copy of your currenty application(on-premise or cloud) with the AWS Resources(EC2, EBS), then continously replicate data with the production. During normal operation, maintain readiness by monitoring replication and periodically performing non-disruptive recovery and failback drills.

## Migration
- AWS Migration Hub is single place to discover existing server, plan migration and track the status of the migration proccess
  - Migration statergy can be rehost, replatform and refactor of the applications.
  - You can import information about on-premises servers and applications, or you can perform a deeper discovery using AWS Discovery Agent or AWS Discovery Collector, an agentless approach for VMware environments.
