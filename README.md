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
- Migration strategy
![migration strategy](https://github.com/user-attachments/assets/9d621ef4-aa9f-4b96-b85d-ab864eee9c76)
- Discovery Agent can not send log to S3, only to Application Discovery Service. In Migration Hub, enable Data Exploration to query data in Athena.
- Application Discovery Service Agentless Collector for VMWare is a virtual machine, which is provided via an OVA file. It needs a IAM user credentials to authenticate with AWS to forward to the Application Discovery Service.
- In DMS, the mapping rules(JSON) should be put in source endpoint config

## Network
- NAT Gateway is only for IPv4. With IPv6, if you want to connect to internet from a private subnet, a egress-only internet gateway should be used.
  - There is no charge for an egress-only internet gateway, but there are data transfer charges for EC2 instances that use internet gateways
- Transit Gateway allow enabling multicast and select subnets to include in the multicast domain when associating VPC attachments.
- Route53 Resolver
  - Inbound endpoints allow DNS queries to your VPC from on-premise network or another VPC
  - Outbound endpoints allow DNS queries from your VPC to on-premise network or another VPC
  - Resolver rules enable you to create one forwarding rule for each domain name and specify the name of the domain for which you want to forward DNS queries from your VPC to an on-premises DNS resolver and from your on-premises to your VPC. Rules are applied directly to your VPC and can be shared across multiple accounts. 

# IoT
- AWS IoT Core helps you connect devices to AWS Services and other devices, secure data interactions, and process and act upon device data.
  - AWS IoT Core provides a fully managed palette of MQTT-based messaging features
- AWS IoT SiteWise is a managed service that makes it easy to collect, organize, and analyze data from industrial equipment at scale.
  - Data collection using SiteWise:
    - AWS IoT SiteWise Edge, on-premises software used to collect, organize, process, and monitor equipment data locally before sending it to AWS.
    - MQ Telemetry Transport (MQTT) protocol integration using AWS IoT Core.
- IoT Analytics is a tool to run and operate analytics on massive volumes of IoT data.
  - It is suitable for analyzing data at rest(S3 or Kinesis Data Streams or directly from IoT Core). Can be used with SQL queries and intergrated with QuickSight 
  - For using IoT Analytics a channel is defined that filters data to be stored and analyzed. The processed data can be stored in time series data storage for futher queries.
- Kinesis Analytics is a suitable service for analyzing streaming data
- IoT 1-click helps to launch AWS Lambda functions from the ready-to-use simple IoT devices. I can also be used to manage these devices from mobile apps or from the console
- IoT Events is a service used to detect and respond to events from IoT sensors. It montors sensors for operational changes and initiates actions to alert users.
  - You can complete an event detector setup in AWS IoT Events, write your event logic using simple ‘if-then-else’ statements, and select the alert or custom action to trigger when the event occurs. 
- AWS IoT TwinMaker is a service that makes it faster and easier to create digital twins of real-world systems and apply them to improve operations. For creating digital twins, following steps needs to take
  - Collect Data from multiple IoT sensors(using AWS IoT SiteWise)
  - Using IoT TwinMaker to create a digital twin from the collected data
    - Create a workspace
    - Associate with the datastore (IoT SiteWise)
      - AWS IoT TwinMaker provides built-in connectors for different data stores, including AWS IoT SiteWise for time-series sensor data, Amazon Kinesis Video Streams for video data, and Amazon Simple Storage Service (S3) for document data. 
    - Using the AWS IoT TwinMaker console-based scene composer, import 3D models (such as CAD files and point cloud scans) to compose scenes, and position the 3D assets to correctly match and represent your physical environment and systems. 
    - Create a web-based digital twin application using the AWS IoT TwinMaker plug-in for Amazon Managed Grafana which build dashboards embedding 3D scences and display data insights about the physical systems
- IoT Device Defender is a tool to audit configs, authenticate devices, detect anomaly and receive alerts to secure IoT device fleet
- IoT Device Management helps register, organize, monitor, and remotely manage IoT devices at scale. Integrate with IoT core to easily connect and manage device.
  - Bulk registe, organize group, update over the air
  - Create a device tunnel - secure remote SSH session to a device installed behind a restricted firewall
  - Define jobs or actions, then run it on selected group of devices
  - 

## Machine Learning
- To import time-series data into Amazon Forecast, the time-series data must be stored in S3
- How to use Fraud Detector
  - Build, train, and deploy an Amazon Fraud Detector model based on historical events
  - Generate fraud predictions
    - Build detector
    - Add model
    - Add rules
    - Configure rule execution and rule order
    - Review and create detector version -> activate
- Amazon Comprehend(Natural-language Processing- NLP) is used to extract insight from documents. For ex, it can detect how customers feel about products

## Security
- Amazon Detective has role session analysis feature that can provide visibility to role usage, cross-account role assumptions, role-chaining activitiese performed across multiple accounts.
- AWS Network Firewall can be used to inspect and control traffice between VPCs or subnets in the same VPC using VPC routing enhancements. 
- AWS Config best practice
  - Enable AWS Config in all accounts and Regions.
  - Record configuration changes to ALL resource types.
  - Record global resources (such as IAM resources) only in one Region.
  - Ensure that you have a secure Amazon S3 bucket to collect the configuration history and snapshot files.
  - Specify an Amazon S3 bucket from another (central IT) account for centralized management of history files and snapshots.
  - Specify an Amazon Simple Notification Service (Amazon SNS) topic from another (central IT) account for centralized management of configuration and compliance notifications.
  - Use Amazon CloudWatch Events to filter AWS Config notifications and take action.
  - Set the appropriate permissions for the IAM role assigned to AWS Config.
    - Use the AWS Config service linked role to allow Config to record resource configuration changes.
    - If you prefer to create an IAM role for AWS Config yourself, use the AWS managed policy AWS_ConfigRole and attach it to your IAM role.
  - Ensure that the SNS topic permissions are restricted to only allow AWS Config to publish messages to it.
  - Turn on periodic snapshots with a minimum frequency of once per day.
  - Use the AWS CloudTrail Lookup API action to find the API events that occurred in the timeframe when the configuration change occurred.
  - If you have your own third party ITSM or CMDB solution like ServiceNow or Jira Service desk, use the AWS Service Management connector to feed Config data into those systems.
  - Identify resources that are undergoing the most configuration changes on a routine basis to control costs.
  - Use Conformance Packs in your account as well as across your organization.
  - Leverage the sample templates for conformance packs as a starting point to quickly bootstrap your accounts.
  - Use AWS Security Hub for an opinionated set of security checks and AWS Config conformance packs for any customization or building your own compliance pack.
  - Use the AWS Config Rule Development Kit (RDK) for authoring custom rules.
  - Create change-triggered custom rules for resource types supported in AWS Config.
  - Create periodic custom rules for resource types not supported in AWS Config.
  - In a multi-account scenario involving custom rules, centralize the Lambda function in one account for easier management.
  - Use the AWS Config Rules repository, a community-based source of custom AWS Config rules.
  - Config rules and conformance packs that have global resources in scope (such as IAM), should only be deployed in one region to avoid costs and API throttling.
  - For custom rules, while submitting put-evaluations, use “annotations” to add supplementary information about how the evaluation determined the compliance.
  - Ensure judicious usage of “DeleteResults” and “Re-evaluate”rules functionalities for your config rules to avoid spike in AWS Config billing.
  - Use the data aggregation feature to aggregate resource configuration and compliance data into a central account.
  - Create an organizations-based aggregator to aggregate AWS Config data from your entire organization.
  - Use the Advanced queries feature to centrally query your resource configuration and compliance data.
  - Use Amazon Athena to query the historical state of your resources.
- IAM -> Organization activity can check last activities on all services in the organization
- AWS Firewall Manager pre-quisites
  - Account must be part of AWS Organization and have enabled all features
  - Firewall Manager must be associate with the management account or associate with a member account that has the appropiate permission
  - AWS Config for each member account
  - (Optional) Enable RAM to centrally config Network Firewall or associate Route53 Resolver DNS Firewall rules across accounts and VPCs

## Others
- Default retetion period of Kinesis DataStream is 24 hours, can be extended up to 365 days.
- There are 2 ways to share database in Data Lake to other accounts
  - Lake Formation Tag-based access control: define perssimsion using attributes, to share Data Catalog resource to external IAM principals, AWS accounts, Organizations and organizational units (OUs)(recommended)
  - Lake Formation named resources: allows you to grant Lake Formation permissions with a grant option on Data Catalog tables and databases to external AWS accounts, IAM principals, organizations, or organizational units. The grant operation automatically shares those resources.
- To run queries against database on other accounts using integrated service such as Athena or Redshift Spectrum, a resource links is required.
- AWS Service Catalog
  - Template constrain: Restrict the configuration parameters that are available for the user when launching the product (for example, EC2 instance types or IP ranges).
  - Launch constraints: Allow you to specify a role for a product in a portfolio. This role is used to provision the resources at launch, so you can restrict user permissions without impacting users’ ability to provision products from the catalog (for example, for marketing users, you can enable them to create campaign websites, but use constraints to restrict their access to provision the underlying databases)
  - Using service actions, you can enable end users to perform operational tasks, troubleshoot issues, run approved commands, or request permissions in AWS Service Catalog on your provisioned products, without needing to grant end users full access to AWS services. You use AWS Systems Manager documents to define service actions.
- AWS Proton is an infrastructure provisioning and deployment service for serverless and container-based applications across multiple accounts. The platform team can use environment templates to create the environment which includes infrastructure service such as VPC, subnets, route tables, etc. With Proton the IAM service role is supplied along with the templates which consist of the permission required to provision resources
  - Infrastructure can be provisioned in one of serveral ways: AWS managed(using CloudFormation), CodeBuild(using CLI, AWS CDK), or self-managed(terraform) 
- Elastic Beanstalk managed update require Update level(Minor and patch or patch only) and Weekly update window to perfome the update. During the update process, the application stay available.
- To enable guest access with Cognito, enable unauthenticated access in Cognito Identity Pool. Then guest users can request an identity ID via GetId API
- Cognito
  - User pool are for authentication(identity verification)
  - Identity pool are for authorization(access control)
- Kinesis Data Firehose destination: S3, Redshift, OpenSearch, HTTP Endpoint(Datadog, New Relic, Splunk, etc), MongoDB
  - With Redshift destination, first Firehose deliver data to intermediate S3 bucket, then load data into Redshift cluster using COPY command. All data will not be deleted after loading
- Output of Kinesis Rekognition should be stored in Kinesis datastream. 
- AWS Transcribe is an automatic speech recognition service that use machine learning models to convert audio to text. Polly is the opposite way(text to speech)
- API Gateway supported response types: https://docs.aws.amazon.com/apigateway/latest/developerguide/supported-gateway-response-types.html
  - When client attemps to invoke unsupported API method or resources, API Gateway will return 403 MISSING_AUTHENTICATION_TOKEN, not 404 by default
