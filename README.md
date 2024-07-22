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

## IoT
- AWS IoT Core helps you connect devices to AWS Services and other devices, secure data interactions, and process and act upon device data.
  - AWS IoT Core provides a fully managed palette of MQTT-based messaging features
- AWS IoT SiteWise is a managed service that makes it easy to collect, organize, and analyze data from industrial equipment at scale.
  - Data collection using SiteWise:
    - AWS IoT SiteWise Edge, on-premises software used to collect, organize, process, and monitor equipment data locally before sending it to AWS.
    - MQ Telemetry Transport (MQTT) protocol integration using AWS IoT Core.
- IoT Analytics is a tool to run and operate analytics on massive volumes of IoT data.
  - It is suitable for analyzing data at rest(S3 or Kinesis Data Streams or directly from IoT Core). Can be used with SQL queries and intergrated with QuickSight 
  - For using Iot Analytics a channel is defined that filters data to be stored and analyzed. The processed data can be stored in time series data storage for futher queries.
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
 
## Others
- Default retetion period of Kinesis DataStream is 24 hours, can be extended up to 365 days.
- There are 2 ways to share database in Data Lake to other accounts
  - Lake Formation Tag-based access control: define perssimsion using attributes, to share Data Catalog resource to external IAM principals, AWS accounts, Organizations and organizational units (OUs)(recommended)
  - Lake Formation named resources: allows you to grant Lake Formation permissions with a grant option on Data Catalog tables and databases to external AWS accounts, IAM principals, organizations, or organizational units. The grant operation automatically shares those resources.
- To run queries against database on other accounts using integrated service such as Athena or Redshift Spectrum, a resource links is required.
